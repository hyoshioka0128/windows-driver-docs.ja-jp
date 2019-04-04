---
title: 修飾および PSHED プラグインを配布します。
description: 修飾および PSHED プラグインを配布します。
ms.assetid: fe6cbb01-552f-4b24-b300-168d6311a596
keywords:
- デジタル署名 WDK WHEA)、PSHED プラグイン
- PSHED プラグインを見極め、WDK WHEA
- PSHED プラグイン WDK WHEA、配布します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 906c41d26fd154203b9ce07efbd8c24d8766ecd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537945"
---
# <a name="qualifying-and-distributing-pshed-plug-ins"></a>修飾および PSHED プラグインを配布します。


品質およびドライバーの整合性を確保するには、プラグインの PSHED をデジタル署名する必要があります。 プラグインの PSHED をデジタル署名するときに、プラットフォーム ベンダーは次のガイドラインに従う必要があります。

-   システムの起動時間を最小限に抑えるには、推奨の埋め込み、 [Authenticode](https://msdn.microsoft.com/library/windows/hardware/ff686697) PSHED プラグイン ファイルにデジタル署名します。 この手順の詳細については、[埋め込みの署名でのドライバーをリリース署名](https://msdn.microsoft.com/library/windows/hardware/ff549832)を参照してください。

-   ハードウェア プラットフォームがサーバーのロゴ テストに追加の検証を受ける前に処理する、プラグインの[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff544840)Windows Hardware Quality Labs (WHQL) デジタル署名が必要です。 このデジタル署名を取得するには、テストし、Unclassified WHQL テスト カテゴリを使用して、ドライバー パッケージを送信する必要があります。

    **注**  WHQL プラグインの PSHED に埋め込まれたかどうかに関係なく、ドライバー パッケージのデジタル署名を取得する必要があります、 [Authenticode](https://msdn.microsoft.com/library/windows/hardware/ff686697)デジタル署名します。

     

プラグインの PSHED をデジタル署名する方法の詳細については、[パブリック リリース用のドライバーの署名](https://msdn.microsoft.com/library/windows/hardware/ff552289)を参照してください。

プラグイン PSHED が WHQL のデジタル署名を取得後、プラグインできますシステム ロゴの認定を要求する任意のシステムで。 サーバーのロゴ認定プロセスの詳細については、[Windows ロゴ プログラム](https://go.microsoft.com/fwlink/p/?linkid=26144)を参照してください。

PSHED プラグインは、「ファミリ」アプローチでは、クラス、またはハードウェア プラットフォームのファミリ間でプラグインの特定の PSHED を展開に修飾する場所を使用して修飾されます。

PSHED プラグインは、ハードウェアのベンダー BIOS およびシステム ファームウェアの更新プログラムを配布する方法と同様の方法でユーザーに配布する必要があります。 また、PSHED プラグインは、プラグインの 1 つの PSHED をハードウェア プラットフォームのファミリ間で展開できるように、プラットフォーム ファームウェアとやり取りする必要があります。

**注**  PSHED プラグインが Windows Update 経由で顧客に配布されません。

 

 

 




