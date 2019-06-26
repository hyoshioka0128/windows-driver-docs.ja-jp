---
title: INF SignatureAttributes セクション
description: このセクションでは、特定の証明書のシナリオで必要な追加の署名を要求することができます。
ms.assetid: 8169686B-C45B-4D67-8B09-CD5F9977898D
keywords:
- INF SignatureAttributes セクションのデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF SignatureAttributes Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02883650cb3b47982d07f5f76b52b90432a621da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370036"
---
# <a name="inf-signatureattributes-section"></a>INF SignatureAttributes セクション


このセクションでは、特定の証明書のシナリオで必要な追加の署名を要求することができます。 たとえば、次のシナリオでは、このセクションが必要です。保護された環境メディアの再生、[起動時マルウェア対策](https://docs.microsoft.com/windows-hardware/drivers/install/elam-driver-submission)、およびサード パーティ製の HAL 拡張機能。 これらの追加の署名は、適切な機能とテストに合格、ハードウェア認定キットのパッケージが含まれている場合にのみ適用されます。

```inf
[SignatureAttributes]
FileOne = SignatureAttributes.SigType

[SignatureAttributes.SigType]
Attribute = Value
```

## <a name="entries"></a>エントリ


<a href="" id="sigtype-signature-type"></a>**SigType =** <em>シグネチャの種類</em>  
ファイルに適用する署名またはカタログ属性ニーズがどのを定義します。 次のいずれかを指定する必要があります。

-   elam
-   HalExt
-   PETrust
-   DRM
-   WindowsHello

<a href="" id="attribute-attribute-name"></a>**属性 =** <em>属性名</em>  
各署名の種類は、次に示すように対応する属性と値。 SignatureAttributes のサブセクションでは、これらの定義を使用します。

-   **SignatureAttributes.Elam**:Elam = true
-   **SignatureAttributes.HalExt**:HalExt = true
-   **SignatureAttributes.DRM**:DRMLevel = {1300 | 1200}
-   **SignatureAttributes.PETrust**:PETrust = true
-   **SignatureAttributes.WindowsHello**:WindowsHello = true

<a name="remarks"></a>注釈
-------

これらの追加の署名は、適切な機能とテストに合格、ハードウェア認定キットのパッケージが含まれている場合にのみ適用されます。 これらは、ハードウェアの認定資格、および Elam、HalExt、PETrust、対応する証明書要件の通常の動作を追加し、DRM が見つかります[ここ](https://go.microsoft.com/fwlink/p/?linkid=239763)します。

ターゲット OS に関係なく、追加の署名を要求するときに、INF セクションではこれらを使用する必要があります。

<a name="examples"></a>例
--------

次の例では、列挙、およびオーディオの追加の署名を要求する方法を示します。

```inf
[SignatureAttributes]
ExampleFile1.dll=SignatureAttributes.PETrust
ExampleFile2.dll=SignatureAttributes.DRM

[SignatureAttributes.DRM]
DRMLevel=1300

 [SignatureAttributes.PETrust]
PETrust=true
```

次の例では、列挙、およびビデオに追加署名を要求する方法を示します。

```inf
[SignatureAttributes]
ExampleFile1.dll=SignatureAttributes.PETrust

[SignatureAttributes.PETrust]
PETrust=true
```

次の例では、列挙および HAL に追加署名を要求する方法を示します。

```inf
[SignatureAttributes]
HALFILE.dll=SignatureAttributes.HalExt

[SignatureAttributes.HalExt]
HalExt=true
```

次の例では、列挙し、ELAM に追加署名を要求する方法を示します。

```inf
[SignatureAttributes]
ELAMFILE.dll=SignatureAttributes.Elam

[SignatureAttributes.Elam]
Elam=true
```

次の例では、列挙、および Windows こんにちはの追加署名を要求する方法を示します。

```inf
[SignatureAttributes]
WindowsHelloFile.dll=SignatureAttributes.WindowsHello

[SignatureAttributes.WindowsHello]
WindowsHello=true
```


## <a name="see-also"></a>関連項目


[ダッシュ ボード ヘルプ](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)

 

 






