---
title: PIN 印刷のサンプル PrintTicket ファイル
description: 暗証番号 (pin) の印刷を指定する方法を示すサンプル PrintTicket ファイルを次に示します。
ms.assetid: FC1BE797-7097-4BEF-A530-3846CED3E400
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc1d54085cece9e86be0710a51e2883d6370b077
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365340"
---
# <a name="sample-printticket-file-for-pin-printing"></a>PIN 印刷のサンプル PrintTicket ファイル


暗証番号 (pin) の印刷を指定する方法を示すサンプル PrintTicket ファイルを次に示します。

```xml
<?xml version="1.0"?>
   <psf:PrintTicket xmlns:psf="http://schemas.microsoft.com/windows/2003/08/printing/printschemaframework" 
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
      xmlns:xsd="http://www.w3.org/2001/XMLSchema" version="1" 
           xmlns:psk="http://schemas.microsoft.com/windows/2003/08/printing/printschemakeywords"
           xmlns:pskv11=" http://schemas.microsoft.com/windows/2013/05/printing/printschemakeywordsv11">
      <psf:ParameterInit name="pskv11:JobPasscodeString">
         <psf:Value xsi:type="xsd:string">123456</psf:Value>
      </psf:ParameterInit>
      <psf:Feature name="pskv11:JobPasscode">
         <psf:Option name="psk:On" />
      </psf:Feature>
   </psf:PrintTicket>
```

保護された印刷の詳細については、次を参照してください。[の保護された印刷ドライバー サポート](driver-support-for-protected-printing.md)します。

 

 




