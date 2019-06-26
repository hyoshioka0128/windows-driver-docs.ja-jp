---
title: バンドル メンバーシップの指定
description: バンドル メンバーシップの指定
ms.assetid: aa73c7fd-a5c8-4ef5-99fd-229fbcc6b4df
keywords:
- 追加レジストリ セクション WDK ネットワー キング、バンドルのメンバーシップ
- バンドルのメンバーシップの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdaa1f7b4bfb2617e9d7f0c9d239bfd405b5354f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383643"
---
# <a name="specifying-bundle-membership"></a>バンドル メンバーシップの指定




> [!NOTE]
> Windows Vista 以降、バンドルのメンバーシップは非推奨とされました。 


インストールする INF ファイル**Net**コンポーネント (物理または仮想ネットワーク アダプター) がそれらのネットワーク アダプターがアダプターの同じバンドルに属していることを指定することができます。 NDIS 中間ドライバ、Net クラスでフィルター ドライバーは、仮想ネットワーク アダプターをエクスポートするが含まれていることに注意してください。 NDIS ドライバーでは、アダプターのバンドルでワークロードを分散することによって、ワークロードのバランスを取るにインストールされたアダプターを使用できます。 負荷分散の詳細については、次を参照してください。[負荷分散とフェールオーバー](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff549197(v=vs.85))します。

アダプターがアダプターの特定のバンドルに属していることを指定するアダプターをインストールするドライバーの INF ファイルを含める必要があります、 **BundleId**キーワードと大文字の文字列値 (REG\_SZ)。 この文字列値は、アダプターのドライバーのバンドルを識別します。 バンドル id 情報を使用して、レジストリが構成されます。

例を次に、*追加レジストリ セクション*を追加するドライバーの INF ファイルで、 **BundleId**にサブキー、 **Ndi\\params**キーとは、**ParamDesc** (パラメーターの説明) の**BundleId** "Bundle1"の文字列値。

```INF
[a1.params.reg]
HKR, Ndi\params\BundleId, ParamDesc, 0, "Bundle1"
```

 

 





