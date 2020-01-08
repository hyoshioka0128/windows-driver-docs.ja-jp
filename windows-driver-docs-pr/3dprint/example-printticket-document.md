---
title: PrintTicket ドキュメント例
description: この例のキーワードは説明のみを目的としていますが、3D 製造用の印刷スキーマキーワードが反映されています。
ms.assetid: 139CF759-0A94-44A5-97BD-4EFD072220EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b75e6028281368e589fa3f3aa5670848c96e6174
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652754"
---
# <a name="printticket-document-example"></a>PrintTicket ドキュメント例


この例のキーワードは説明のみを目的としていますが、3D 製造用の印刷スキーマキーワードが反映されています。 この PrintTicket は、 [PrintCapabilities ドキュメントの例](example-printcapabilities-document.md)によって表される仮想的なデバイス専用に構築されています。

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<psf:PrintTicket
    xmlns:psf="https://schemas.microsoft.com/windows/2003/08/printing/printschemaframework"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xmlns:xsd="https://www.w3.org/2001/XMLSchema" version="1"
    xmlns:ns0000="https://schemas.microsoft.com/windows/printing/oemdriverpt/3dprinter"
    xmlns:psk="https://schemas.microsoft.com/windows/2003/08/printing/printschemakeywords"
    xmlns:psk3d="https://schemas.microsoft.com/3dmanufacturing/2013/01/pskeywords3d"
    xmlns:vnd="https://foo">

    <psf:ParameterInit name="vnd:Job3DAMap">
        <psf:Value xsi:type="xsd:string">1:0</psf:Value>
    </psf:ParameterInit>
    <psf:ParameterInit name="vnd:Job3DBMap">
        <psf:Value xsi:type="xsd:string">1:1</psf:Value>
    </psf:ParameterInit>

    <psf:Feature name="psk3d:Job3DSupports">
        <psf:Option name="psk3d:SupportsIncluded" />
    </psf:Feature>
    <psf:ParameterInit name="psk3d:Job3DSupportsMaterial">
        <psf:Value xsi:type="xsd:QName">vnd:B</psf:Value>
    </psf:ParameterInit>

    <psf:Feature name="psk3d:Job3DRaft">
        <psf:Option name="psk3d:RaftIncluded" />
    </psf:Feature>
    <psf:ParameterInit name="psk3d:Job3DRaftMaterial">
        <psf:Value xsi:type="xsd:QName">vnd:B</psf:Value>
    </psf:ParameterInit>

    <psf:Feature name="psk3d:Job3DQuality">
        <psf:Option name="psk3d:Medium" />
    </psf:Feature>
    <psf:Feature name="psk3d:Job3DDensity">
        <psf:Option name="psk3d:Low"/>
    </psf:Feature>
    
</psf:PrintTicket>
```

 

 




