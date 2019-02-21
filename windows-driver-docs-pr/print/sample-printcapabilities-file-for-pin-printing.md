---
title: サンプル PrintCapabilities ファイルの暗証番号 (pin) の印刷
description: ここでは、保護された印刷の個人 ID 番号 (PIN) を指定する方法を示すサンプル PrintCapabilities ファイル。
ms.assetid: 4C3BBEF1-C0DB-48F7-B4EC-BBB5D3699692
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1c674cdd09328183a57ede8759c07e46ea6f622
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550534"
---
# <a name="sample-printcapabilities-file-for-pin-printing"></a>サンプル PrintCapabilities ファイルの暗証番号 (pin) の印刷


ここでは、保護された印刷の個人 ID 番号 (PIN) を指定する方法を示すサンプル PrintCapabilities ファイル。

```xml
<?xml version="1.0"?>
<psf:PrintCapabilities
   xmlns:psf="http://schemas.microsoft.com/windows/2003/08/printing/printschemaframework" 
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
   xmlns:xsd="http://www.w3.org/2001/XMLSchema" version="1"
   xmlns:psk="http://schemas.microsoft.com/windows/2003/08/printing/printschemakeywords"
   xmlns:pskv11=" http://schemas.microsoft.com/windows/2013/05/printing/printschemakeywordsv11">
   <psf:ParameterDef name="pskv11:JobPasscodeString">
      <psf:Property name="psf:DataType">
           <psf:Value xsi:type="xsd:QName">xsd:string</psf:Value>
      </psf:Property>
      <psf:Property name="psf:DefaultValue">
           <psf:Value xsi:type="xsd:string"/>
      </psf:Property>
      <psf:Property name="psf:MaxLength">
           <psf:Value xsi:type="xsd:integer">9</psf:Value>
      </psf:Property>
      <psf:Property name="psf:MinLength">
           <psf:Value xsi:type="xsd:integer">4</psf:Value>
      </psf:Property>
      <psf:Property name="psf:Mandatory">
              <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
      </psf:Property>
      <psf:Property name="psf:UnitType">
              <psf:Value xsi:type="xsd:string">numeric</psf:Value>
      </psf:Property>
      <psf:Property name="psk:DisplayName">
           <psf:Value xsi:type="xsd:string">Job PassCode</psf:Value>
      </psf:Property>
   </psf:ParameterDef>
   <psf:Feature name="pskv11:JobPasscode">
      <psf:Property name="psf:SelectionType">
           <psf:Value xsi:type="xsd:string">psk:PickOne</psf:Value>
      </psf:Property>
      <psf:Property name="psk:DisplayName">
           <psf:Value xsi:type="xsd:string">Enable Job PassCode</psf:Value>
      </psf:Property>
      <psf:Option name="psk:On" />
      <psf:Option name="psk:Off" />
   </psf:Feature>
</psf:PrintCapabilities>
```

保護された印刷の詳細については、次を参照してください。[ドライバー サポートの保護された印刷](driver-support-for-protected-printing.md)します。

 

 




