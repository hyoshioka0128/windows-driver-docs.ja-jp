---
title: テレビ コネクタとコピー防止のハードウェアのクエリを実行します。
description: テレビ コネクタとコピー防止のハードウェアのクエリを実行します。
ms.assetid: 7812a3ba-42f1-4872-bfe8-08933802f0c1
keywords:
- テレビ コネクタ WDK ビデオのミニポート
- コピー防止の WDK のビデオのミニポート、クエリを実行します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cf18cf5d08535313b9d5bd990595ffb6ae6bb78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551037"
---
# <a name="querying-tv-connector-and-copy-protection-hardware"></a>テレビ コネクタとコピー防止のハードウェアのクエリを実行します。


## <span id="ddk_querying_tv_connector_and_copy_protection_hardware_gg"></span><span id="DDK_QUERYING_TV_CONNECTOR_AND_COPY_PROTECTION_HARDWARE_GG"></span>


テレビ コネクタがあるアダプターのビデオのミニポート ドライバーを処理する必要があります、 [ **IOCTL\_ビデオ\_処理\_VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff567805)要求でその[ *HwVidStartIO* ](https://msdn.microsoft.com/library/windows/hardware/ff567367)関数。 ときに、IOCTL 要求は、IOCTL\_ビデオ\_処理\_VIDEOPARAMETERS、 **InputBuffer**のメンバー、 [**ビデオ\_要求\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff570547)へのポインターを構造体、 [ **VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff570173)構造体。 **DwCommand** VIDEOPARAMETERS 構造体のメンバーでは、ミニポート ドライバーがテレビ コネクタに関する情報を提供する必要があるかどうかを指定します (VP\_コマンド\_取得) または TV に指定した設定を適用コネクタ (担当副社長\_コマンド\_設定)。

ときに、 **dwCommand** VIDEOPARAMETERS 構造体のメンバーは担当副社長\_コマンド\_GET、ミニポート ドライバーでは、次を実行する必要があります。

-   確認、 **Guid** VIDEOPARAMETERS 構造体のメンバー。

-   テレビ コネクタでサポートされる機能ごと対応するフラグを設定する、 **dwFlags** VIDEOPARAMETERS 構造体のメンバー。

-   各フラグ設定、 **dwFlags**メンバー、機能とそのフラグに関連付けられている現在の設定を示す VIDEOPARAMETERS 構造体の対応するメンバーに値を代入します。 参照してください、 [ **VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff570173)リファレンス ページの特定のフラグに対応する構造体のメンバーの一覧。

**寸法**VIDEOPARAMETERS 構造体のメンバーでは、テレビがビデオの再生または Windows デスクトップを表示するために最適化を出力するかどうかを指定します。 ビデオの値を\_モード\_テレビ\_再生、テレビは、ビデオの再生に適した出力を指定します (つまり、ちらつきのフィルターが無効になっていますおよびオーバーが有効になっている)。 ビデオの値を\_モード\_WIN\_グラフィックスでは、テレビは、Windows グラフィックス用に最適化された出力を指定します (は、最大ちらつきフィルターが有効になっているし、オーバー スキャンが無効になっています)。

担当副社長への応答で\_コマンド\_GET、ミニポート ドライバーでは、担当副社長を設定する必要があります\_フラグ\_テレビ\_モード フラグ**dwFlags** 、担当副社長を設定する必要があります\_モード\_WIN\_グラフィックス ビット**dwAvailableModes**します。 設定、担当副社長\_モード\_テレビ\_再生ビット**dwAvailableModes**は省略可能です。 さらに、ミニポート ドライバーは、担当副社長を設定する必要があります\_フラグ\_最大\_でフラグを調整**dwFlags** VIDEOPARAMETERS 構造体の対応するメンバーに値を代入する必要があります。

担当副社長への応答で\_コマンド\_ミニポート ドライバーを設定する必要があります、テレビの出力が現在無効になっている場合は、GET、**寸法**を 0 に設定**dwTVStandard**担当副社長に\_標準\_WIN\_VGA、設定と**dwAvailableTVStandard**担当副社長に\_標準\_WIN\_VGA します。

例 1:アダプターは、現在無効になっているテレビ出力をサポートします。 ミニポート ドライバーは、担当副社長への応答では、次を行う必要があります\_コマンド\_を取得します。

-   **DwFlags**、担当副社長設定\_フラグ\_テレビ\_モードでは、担当副社長\_フラグ\_テレビ\_STANDARD、およびテレビでサポートされている機能を表すその他のすべてのフラグコネクタです。

-   設定**寸法**を 0 にします。

-   **DwAvailableModes**、担当副社長設定\_モード\_WIN\_グラフィックス。 ハードウェアは、担当副社長をサポートしている場合\_モード\_テレビ\_ビットも再生を設定します。

-   設定**dwTVStandard**担当副社長に\_テレビ\_標準\_WIN\_VGA します。

-   **DwAvailableTVStandard**、テレビ コネクタでサポートされるテレビ標準を表すすべてのビットを設定します。

-   すべてのフラグがセット**dwFlags** (担当副社長以外\_フラグ\_テレビ\_モードと担当副社長\_フラグ\_テレビ\_STANDARD で、既に説明しました)、割り当てるVIDEOPARAMETERS 構造体の対応するメンバーの値です。

例 2:テレビの出力を有効にするのには、呼び出し元 (ミニポート ドライバーではなく) が、以下を実行しました。

-   **DwFlags**、担当副社長設定\_フラグ\_テレビ\_モードと担当副社長\_フラグ\_テレビ\_標準。 その他のすべてのフラグをオフにします。

-   設定**寸法**か担当副社長に\_モード\_WIN\_グラフィックスや担当副社長\_モード\_テレビ\_再生します。 両方のビットを設定しないでください。

-   設定**dwTvStandard**標準を目的に (たとえば VP\_テレビ\_標準\_NTSC\_M)。 その他のすべてのビットを設定しないでください**dwTvStandard**します。

例 3: テレビの出力を無効にするには、呼び出し元 (ミニポート ドライバーではなく) が、以下を実行します。

-   **DwFlags**、担当副社長設定\_フラグ\_テレビ\_モードと担当副社長\_フラグ\_テレビ\_標準。 その他のすべてのフラグをオフにします。

-   設定**寸法**を 0 にします。

-   **DwTvStandard**、担当副社長設定\_テレビ\_標準\_WIN\_VGA します。 その他のすべてのビットをオフに**dwTvStandard**します。

 

 





