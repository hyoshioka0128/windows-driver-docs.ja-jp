---
title: テレビ コネクタとコピー保護、ビデオのミニポート ドライバーには
description: テレビ ミニポート ドライバーでのテレビ コネクタおよびコピー防止サポート
ms.assetid: 7d7d44b5-3248-4bee-bc4d-e02fd3c606a7
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、テレビ コネクタ
- ビデオのミニポート ドライバー WDK Windows 2000 では、コピー防止のサポートします。
- テレビ コネクタ WDK ビデオのミニポート
- コピー防止 WDK ビデオのミニポート
- IOCTL_VIDEO_HANDLE_VIDEOPARAMETERS
- コピー防止 WDK ビデオのミニポート、コピー保護のサポートについて
- ハードウェアの WDK コピー防止
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 07a3751eaa0e47f25cb997ed32dacb577a25385d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389777"
---
# <a name="tv-connector-and-copy-protection-support-in-video-miniport-drivers"></a>テレビ ミニポート ドライバーでのテレビ コネクタおよびコピー防止サポート

テレビ コネクタがあるアダプターのビデオのミニポート ドライバーを処理する必要があります[ **VRPs** ](https://msdn.microsoft.com/library/windows/hardware/ff570547)で、 [ **IOCTL\_ビデオ\_ハンドル\_VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff567805) I/O 制御コード。 この IOCTL は、機能およびテレビ コネクタとコピー防止のハードウェアの現在の設定を照会するか、テレビのコネクタとコピー防止のハードウェアの機能を設定するには、ミニポート ドライバーに送信されます。 ミニポート ドライバーをチェックして実行するアクションを決定する、 **dwCommand**のフィールド、 [ **VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff570173) VRP ので渡される構造体**InputBuffer**します。 システムでは、ミニポート ドライバーはこの VRP を処理しない場合、Rovi (旧称 Macrovision) の再生が Dvd を保護することはできません。

場合**dwCommand**担当副社長に設定されている\_コマンド\_GET、およびデバイス*しない*ミニポート ドライバーは、NO を返す必要があります、出力、テレビをサポート\_のエラー**ステータス**VRP のメンバー **StatusBlock**します。 これを設定する必要がありますも、**情報**VRP のメンバー **StatusBlock**サイズ (バイト単位) を VIDEOPARAMETERS の構造体します。 設定する必要があります**dwFlags**を 0 に設定**dwTVStandard**担当副社長に\_テレビ\_標準\_WIN\_VGA、設定と**dwAvailableTVStandard**担当副社長に\_テレビ\_標準\_WIN\_VGA します。

場合**dwCommand**担当副社長に設定されている\_コマンド\_GET、およびデバイス*は*TV の出力のサポート、ミニポート ドライバーが示されますこの VIDEOPARAMETERS 構造に設定して、フラグを適切な**dwFlags**メンバーと設定フラグに対応するその他の構造体メンバーに値を割り当てることで。

次のセクションでは、テレビのコネクタがあるデバイスのミニポート ドライバーの実装の詳細を説明します。

[テレビ コネクタとコピー防止のハードウェアのクエリを実行します。](querying-tv-connector-and-copy-protection-hardware.md)

[コピー防止のハードウェアの設定](setting-copy-protection-hardware.md)

 

 





