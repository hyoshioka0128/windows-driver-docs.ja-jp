---
title: 不変な MDL のスタック用検査
description: 不変な Mdl スタック用検査オプションは、ドライバーがドライバー スタック間で不変の MDL バッファーを処理する方法を監視します。
ms.assetid: AB27803A-6B3A-40FA-B962-79B0DA2F5FA9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 173c8e9266184942287b4d588479275bd56566e0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373709"
---
# <a name="invariant-mdl-checking-for-stack"></a>不変な MDL のスタック用検査


不変な Mdl スタック用検査オプションは、ドライバーがドライバー スタック間で不変の MDL バッファーを処理する方法を監視します。 不変の MDL バッファーに対する無効な改変が、ドライバーの検証ツールによって検出されます。 このオプションを使うには、少なくとも 1 つのドライバーで I/O の検証を有効にする必要があります。

**注**  このオプションは Windows 8 以降で使用できます。

 

不変な Mdl オプションでは、不変の MDL バッファー ポイントでのみ、要求のドライバーの規則に従うことにより、スタックのドライバー スタックを離れることができます。

不変の MDL が に表示されるの IRP を初めて、 [**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver) 、日常的な一意のシグネチャは不変の MDL バッファーの内容から計算し、内部のデータベースに格納されています。 内の IRP の完了時に、 [ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)バッファーが変更されていない場合は、署名を記録された不変の MDL 保持 IRP 日常的な Driver Verifier 検証します。

IRP の有効期間全体を通じて、書き込み要求の不変のバッファーを変更できません。 読み取り要求の場合、インバリアント バッファーは変更できませんのディスパッチ パスのバッファーの署名の比較は、最後の呼び出しに行われるように[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)します。

不変な Mdl スタック用検査オプションは、スタック内の個々 のドライバーに渡されますバッファーへの動作に関係なく、全体のドライバー スタック間で MDL バッファーの不変性を確認します。 このオプションは、グローバル - ドライバーごとに選択的に適用することはできません。 不変な Mdl スタック用検査オプションのみをキャッチできます違反、バッファーの不変性を冒とくしたドライバーを特定できません。 障害のあるドライバーを特定できるように、使用、[不変な Mdl のドライバー](invariant-mdl-checking-for-driver.md)オプションで、呼び出しごとにコンテンツ バッファーの不変性の検証を行う[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)と[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) Ddi します。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。


ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用してに不変な Mdl のスタック機能の 1 つまたは複数のドライバーをアクティブにできます。 不変な Mdl スタック用検査オプションがアクティブまたは非アクティブにコンピューターを再起動する必要があります。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。

不変な Mdl スタック用検査オプションをアクティブ化する必要がありますもアクティブ化する[I/O の検証](i-o-verification.md)です。

-   **コマンドラインで**

    、コマンドラインで不変な Mdl のスタックで表される**0x00002000** (ビット 13)。 不変な Mdl のスタックを有効にするには、0x00002010 のフラグの値を使用して、または 0x00002010 をフラグ値に追加します。 この値には、I/O の検証 (0x10) と不変な Mdl のスタック (0x00002000) がアクティブにします。 次に、例を示します。

    ```
    verifier /flags 0x00002010 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

-   **ドライバー検証マネージャーを使用します。**
    1.  ドライバー検証マネージャーを起動します。 型**Verifier**コマンド プロンプト ウィンドウでします。
    2.  選択 **(コード開発者) 用のカスタム設定を作成する** をクリックし、 **次へ。**
    3.  選択**完全な一覧から個々 の設定を選択します。** します。
    4.  選択 (チェック) [I/O の検証](i-o-verification.md)不変な Mdl のスタックとします。
    5.  コンピューターを再起動します。

 

 





