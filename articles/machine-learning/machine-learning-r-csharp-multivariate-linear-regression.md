---
title: 多變量線性迴歸 | Microsoft Docs
description: 多變量線性迴歸
services: machine-learning
documentationcenter: ''
author: jaymathe
manager: jhubbard
editor: cgronlun

ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/14/2016
ms.author: jaymathe

---
# 多變量線性迴歸
假設您有一個資料集，並想要根據獨立變數，快速地預測每個項目 (i) 的相依變數 (y)。線性迴歸是這類預測的常用統計技術。這裡假設相依變數 y 是連續值。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

一個簡單的案例是研究人員嘗試根據身高 (x) 來預測某人 (y) 的體重。一個較為進階的案例是研究人員擁有個別的額外資訊 (例如體重、性別、種族)，並嘗試預測某人的體重。這項 [Web 服務](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression)會將資料套入線性迴歸模型，並為資料中的每個觀察輸出預測值 (y)。

> 使用者可透過行動裝置應用程式、網站，甚至是本機電腦，來取用這項 Web 服務。不過，該 Web 服務也可用來示範如何使用 Azure Machine Learning，來建立採用 R 程式碼的 Web 服務。只需幾行 R 程式碼並在 Azure Machine Learning Studio 中的按鈕上按幾下，就可以建立採用 R 程式碼的實驗，並將其發佈為 Web 服務。接著可將 Web 服務發佈至 Azure Marketplace，以供世界各地的使用者和裝置取用，而不需要 Web 服務的作者設定基礎結構。
> 
> 

## 使用 Web 服務
此 web 服務會根據所有觀察的獨立變數來提供相依變數的預測值。Web 服務需要使用者以字串形式輸入資料，其中資料列會以逗號 (,) 分隔，而資料行會以分號 (;) 分隔。Web 服務一次可輸入一個資料列，而且第一個資料行必須是相依變數。範例資料集看起來可能像這樣：

![範例資料][1]

沒有相依變數的觀察應輸入 “NA” 做為 y。上述資料集的資料輸入字串如下：“10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”。輸出會是根據獨立變數的每個資料列預估值。

> 在 Azure Marketplace 上託管的這項服務是一個 OData 服務，可透過 POST 或 GET 方法進行呼叫。
> 
> 

以自動化方式取用服務的方法有很多種 ([這裡](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)提供一個範例應用程式)。

### 啟動 Web 服務使用的 C# 程式碼：
    public class Input
    {
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { value = TextBox1.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




## 建立 Web 服務
> 這項 Web 服務是使用 Azure Machine Learning 所建立。如需免費試用版，以及有關建立實驗和[發佈 Web 服務](machine-learning-publish-a-machine-learning-web-service.md)的簡介影片，請參閱 [azure.com/ml](http://azure.com/ml)。以下是建立 Web 服務之實驗的螢幕擷取畫面，以及實驗內每個模組的範例程式碼。
> 
> 

Azure Machine Learning 中已建立新的空白實驗，並將兩個[執行 R 指令碼][execute-r-script]模組提取到工作區。這項 Web 服務使用基礎 R 指令碼來執行 Azure Machine Learning 實驗。這項實驗有兩個部分：結構描述定義，以及定型模型 + 計分。第一個模組會定義輸入資料集的預期結構，其中第一個變數是相依變數，而其餘變數是獨立變數。第二個模組會將輸入資料套入一般線性迴歸模型。

![實驗流程][3]

#### 模組 1：
#### 結構描述定義
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### 模組 2：
#### LM 模型
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## 限制
這是一個非常簡單的多元線性迴歸 Web 服務案例。從上面的範例程式碼可以看出，未實作錯誤攔截，且由於建立這項 Web 服務時，服務只輸入數值，因此服務會假設所有項目都是連續變數 (不允許類別功能)。此外，由於 Web 服務呼叫的要求/回應本質，以及每次呼叫 Web 服務時就會調整模型的事實，該項服務目前只能處理有限的資料大小。

## 常見問題集
如需取用 Web 服務或發佈至 Azure Marketplace 的常見問題集，請參閱[這裡](machine-learning-marketplace-faq.md)。

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/


<!---HONumber=AcomDC_0921_2016-->