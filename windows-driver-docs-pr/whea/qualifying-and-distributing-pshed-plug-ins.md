---
title: PSHED プラグインの認定と配布
description: PSHED プラグインの認定と配布
ms.assetid: fe6cbb01-552f-4b24-b300-168d6311a596
keywords:
- デジタル署名 WDK WHEA)、PSHED プラグイン
- PSHED プラグインを見極め、WDK WHEA
- PSHED プラグイン WDK WHEA、配布します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f409665dc7d3f3890032e1bc2fee31f16671a189
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387154"
---
# <a name="qualifying-and-distributing-pshed-plug-ins"></a>PSHED プラグインの認定と配布


品質およびドライバーの整合性を確保するには、プラグインの PSHED をデジタル署名する必要があります。 プラグインの PSHED をデジタル署名するときに、プラットフォーム ベンダーは次のガイドラインに従う必要があります。

-   システムの起動時間を最小限に抑えるには、推奨の埋め込み、 [Authenticode](https://docs.microsoft.com/windows-hardware/drivers/install/authenticode) PSHED プラグイン ファイルにデジタル署名します。 この手順の詳細については、次を参照してください。[埋め込みの署名でのドライバーをリリース署名](https://docs.microsoft.com/windows-hardware/drivers/install/release-signing-a-driver-through-an-embedded-signature)します。

-   ハードウェア プラットフォームがサーバーのロゴ テストに追加の検証を受ける前に処理する、プラグインの[ドライバー パッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)Windows Hardware Quality Labs (WHQL) デジタル署名が必要です。 このデジタル署名を取得するには、テストし、Unclassified WHQL テスト カテゴリを使用して、ドライバー パッケージを送信する必要があります。

    **注**  WHQL プラグインの PSHED に埋め込まれたかどうかに関係なく、ドライバー パッケージのデジタル署名を取得する必要があります、 [Authenticode](https://docs.microsoft.com/windows-hardware/drivers/install/authenticode)デジタル署名します。

     

プラグインの PSHED をデジタル署名する方法の詳細については、次を参照してください。[パブリック リリース用のドライバーの署名](https://docs.microsoft.com/windows-hardware/drivers/install/signing-drivers-for-public-release--windows-vista-and-later-)します。

プラグイン PSHED が WHQL のデジタル署名を取得後、プラグインできますシステム ロゴの認定を要求する任意のシステムで。 サーバーのロゴ認定プロセスの詳細については、次を参照してください。 [Windows ロゴ プログラム](https://go.microsoft.com/fwlink/p/?linkid=26144)します。

PSHED プラグインは、「ファミリ」アプローチでは、クラス、またはハードウェア プラットフォームのファミリ間でプラグインの特定の PSHED を展開に修飾する場所を使用して修飾されます。

PSHED プラグインは、ハードウェアのベンダー BIOS およびシステム ファームウェアの更新プログラムを配布する方法と同様の方法でユーザーに配布する必要があります。 また、PSHED プラグインは、プラグインの 1 つの PSHED をハードウェア プラットフォームのファミリ間で展開できるように、プラットフォーム ファームウェアとやり取りする必要があります。

**注**  PSHED プラグインが Windows Update 経由で顧客に配布されません。

 

 

 




