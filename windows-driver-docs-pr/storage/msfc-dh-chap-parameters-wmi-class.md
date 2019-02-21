---
title: MSFC\_DH\_Chap\_パラメーター WMI クラス
description: MSFC\_DH\_Chap\_パラメーター WMI クラス
ms.assetid: 259E3935-0F37-4DBE-BED3-C55A6715A810
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9cbe71379f0364f7521fe2752164d4a9d1a46b14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550328"
---
# <a name="msfcdhchapparameters-wmi-class"></a>MSFC\_DH\_Chap\_パラメーター WMI クラス


WMI クライアントを使用して、 **MSFC\_DH\_Chap\_パラメーター**仮想ポートに CHAP チャレンジ応答のパラメーターを設定するクラス。

**MSFC\_DH\_Chap\_パラメーター**クラスが次のように定義されている*Npivwmi.mof*:

```mof
class MSFC_DH_Chap_Parameters
{    
    [WmiDataId(1),
     Description("Length in bytes of the shared secret."):Amended]
    uint32 SharedSecretLength;
   
    [WmiDataId(2),
    Description("Shared Secret Encoding"):Amended,
     ValueMap {"1", "2"},
     Values {"Printable ASCII", "Binary"}]
    uint8 SecretEncoding;

    [WmiDataId(3),
     WmiSizeIs("SharedSecretLength"),
     Description("Shared secret to be used at the basis of a DH-CHAP challenge."):Amended]
    uint8 SharedSecret[];
};
```

WMI ツール スイートによってコンパイルされると、このクラスの定義には、次のデータ構造が生成されます。

**MSFC\_DH\_Chap\_パラメーター**

この WMI クラスに関連付けられているメソッドはありません。

 

 





