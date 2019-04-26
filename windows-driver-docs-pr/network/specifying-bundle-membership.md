---
title: バンドル メンバーシップの指定
description: バンドル メンバーシップの指定
ms.assetid: aa73c7fd-a5c8-4ef5-99fd-229fbcc6b4df
keywords:
- 追加レジストリ セクション WDK ネットワー キング、バンドルのメンバーシップ
- バンドルのメンバーシップの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86d05b309142d200f4cee8f9ba7fcfcb259e6512
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342580"
---
# <a name="specifying-bundle-membership"></a>バンドル メンバーシップの指定




> [!NOTE]
> Windows Vista 以降、バンドルのメンバーシップは非推奨とされました。 


インストールする INF ファイル**Net**コンポーネント (物理または仮想ネットワーク アダプター) がそれらのネットワーク アダプターがアダプターの同じバンドルに属していることを指定することができます。 NDIS 中間ドライバ、Net クラスでフィルター ドライバーは、仮想ネットワーク アダプターをエクスポートするが含まれていることに注意してください。 NDIS ドライバーでは、アダプターのバンドルでワークロードを分散することによって、ワークロードのバランスを取るにインストールされたアダプターを使用できます。 負荷分散の詳細については、次を参照してください。[負荷分散とフェールオーバー](https://msdn.microsoft.com/library/windows/hardware/ff549197)します。

アダプターがアダプターの特定のバンドルに属していることを指定するアダプターをインストールするドライバーの INF ファイルを含める必要があります、 **BundleId**キーワードと大文字の文字列値 (REG\_SZ)。 この文字列値は、アダプターのドライバーのバンドルを識別します。 バンドル id 情報を使用して、レジストリが構成されます。

例を次に、*追加レジストリ セクション*を追加するドライバーの INF ファイルで、 **BundleId**にサブキー、 **Ndi\\params**キーとは、**ParamDesc** (パラメーターの説明) の**BundleId** "Bundle1"の文字列値。

```INF
[a1.params.reg]
HKR, Ndi\params\BundleId, ParamDesc, 0, "Bundle1"
```

 

 





