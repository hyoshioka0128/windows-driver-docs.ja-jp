---
title: INF SignatureAttributes セクション
description: このセクションでは、ユーザーが特定の認定シナリオに応じて追加の署名を要求できるようにします。
ms.assetid: 8169686B-C45B-4D67-8B09-CD5F9977898D
keywords:
- INF SignatureAttributes セクションデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF SignatureAttributes Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fb6ae4da095e1a830f4e0318d9d738de9bd026d
ms.sourcegitcommit: 5b0d2b7a3a4efa3bc4f94a769bf41d58d3321d50
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72390719"
---
# <a name="inf-signatureattributes-section"></a>INF SignatureAttributes セクション


このセクションでは、ユーザーが特定の認定シナリオに応じて追加の署名を要求できるようにします。 たとえば、次のシナリオでは、保護された環境のメディア再生、[起動時マルウェア対策](https://docs.microsoft.com/windows-hardware/drivers/install/elam-driver-submission)、およびサードパーティの HAL 拡張が必要です。 これらの追加の署名は、ハードウェア認定キットパッケージに適切な機能が含まれ、テストに合格している場合にのみ適用されます。

```inf
[SignatureAttributes]
FileOne = SignatureAttributes.SigType

[SignatureAttributes.SigType]
Attribute = Value
```

## <a name="entries"></a>エントリ


<a href="" id="sigtype-signature-type"></a>**Sigtype =** <em>signature-type</em>  
ファイルに適用する必要がある署名またはカタログ属性を定義します。 次のいずれかを指定する必要があります。

-   Elam
-   HalExt
-   PETrust
-   IRM
-   WindowsHello

<a href="" id="attribute-attribute-name"></a>**属性 =** <em>属性名</em>  
各シグネチャ型には、次に示すように、対応する属性と値があります。 SignatureAttributes サブセクションには、次の定義を使用します。

-   **Signatureattributes。 elam**: elam = true
-   **Signatureattributes. HalExt**: HalExt = true
-   **Signatureattributes。 DRM**: drmlevel = {1300 | 1200}
-   **Signatureattributes。 petrust**: petrust = true
-   **Signatureattributes. WindowsHello**: WindowsHello = true

<a name="remarks"></a>注釈
-------

これらの追加の署名は、ハードウェア認定キットパッケージに適切な機能が含まれ、テストに合格している場合にのみ適用されます。 これらは、ハードウェア認定の通常の動作に加え、Elam、HalExt、PETrust、および DRM に対応する認定要件にも追加されています。 詳しくは、「 [Windows ハードウェア ラボ キット](https://docs.microsoft.com/windows-hardware/test/hlk/)」をご覧ください。

これらの INF セクションは、ターゲット OS に関係なく追加の署名を要求するときに使用する必要があります。

<a name="examples"></a>例
--------

次の例では、オーディオの追加の署名を列挙して要求する方法を示しています。

```inf
[SignatureAttributes]
ExampleFile1.dll=SignatureAttributes.PETrust
ExampleFile2.dll=SignatureAttributes.DRM

[SignatureAttributes.DRM]
DRMLevel=1300

 [SignatureAttributes.PETrust]
PETrust=true
```

次の例は、ビデオの追加の署名を列挙して要求する方法を示しています。

```inf
[SignatureAttributes]
ExampleFile1.dll=SignatureAttributes.PETrust

[SignatureAttributes.PETrust]
PETrust=true
```

次の例は、HAL の追加の署名を列挙して要求する方法を示しています。

```inf
[SignatureAttributes]
HALFILE.dll=SignatureAttributes.HalExt

[SignatureAttributes.HalExt]
HalExt=true
```

次の例では、ELAM の追加の署名を列挙して要求する方法を示しています。

```inf
[SignatureAttributes]
ELAMFILE.dll=SignatureAttributes.Elam

[SignatureAttributes.Elam]
Elam=true
```

次の例は、Windows Hello の追加の署名を列挙して要求する方法を示しています。

```inf
[SignatureAttributes]
WindowsHelloFile.dll=SignatureAttributes.WindowsHello

[SignatureAttributes.WindowsHello]
WindowsHello=true
```


## <a name="see-also"></a>関連項目


[ダッシュボードのヘルプ](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)

 

 






