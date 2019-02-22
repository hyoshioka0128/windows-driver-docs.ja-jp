---
title: 保護されたビデオ セッションを開始します。
description: 保護されたビデオ セッションを開始します。
ms.assetid: c92f2d1a-ac15-49d4-858b-ff207ff4810c
keywords:
- コピー防止 WDK COPP、保護されたビデオ セッションを開始します。
- ビデオのコピー防止 WDK COPP、保護されたビデオ セッションを開始します。
- COPP WDK DirectX va なので、以降のビデオ セッションを保護します。
- セッションを開始する、保護対象のビデオの WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ecca5754a3df8e0857d69de15de968fde21e59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558750"
---
# <a name="starting-a-protected-video-session"></a>保護されたビデオ セッションを開始します。


## <span id="ddk_starting_a_protected_video_session_gg"></span><span id="DDK_STARTING_A_PROTECTED_VIDEO_SESSION_GG"></span>


**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

保護されたビデオ セッションを開始するには、VMR は特定の順序で DirectX VA COPP デバイスでの操作を開始する必要があります。 この順序に従わない場合、ビデオのミニポート ドライバーがエラー コード E を返す必要があります\_予期しません。 ビデオのミニポート ドライバーが COPP デバイスに操作が実行されると、一意のデバイスの状態の定数を割り当てることで、それ以降を実行する前に、デバイスの状態の定数を確認することでし、適切な操作順序に従うことを確認することができます。操作です。

保護されたビデオ セッションを開始するには、次の順序で COPP デバイスの機能に呼び出しが行われます。

1.  [ *COPPOpenVideoSession* ](https://msdn.microsoft.com/library/windows/hardware/ff539650) COPP デバイスを初期化します。 、戻る前に、ドライバーは、COPP にデバイスの状態の定数を設定する必要があります\_OPENED します。

2.  [ *COPPGetCertificateLength* ](https://msdn.microsoft.com/library/windows/hardware/ff539644)グラフィックス ハードウェアで使用される証明書のバイト単位のサイズを取得します。 ドライバーがデバイス状態の定数が現在 COPP に設定することを確認する必要がありますまず\_OPENED します。 ドライバーを返す必要がありますそれがないかどうか、E\_予期しません。 、戻る前に、ドライバーは、COPP にデバイスの状態の定数を設定する必要があります\_CERT\_長さ\_から返されました。

3.  [ *COPPKeyExchange* ](https://msdn.microsoft.com/library/windows/hardware/ff539646)グラフィックス ハードウェアで使用されるデジタル証明書を取得します。 ドライバーがデバイス状態の定数が現在 COPP に設定することを確認する必要がありますまず\_CERT\_長さ\_から返されました。 ドライバーを返す必要がありますそれがないかどうか、E\_予期しません。 、戻る前に、ドライバーは、COPP にデバイスの状態の定数を設定する必要があります\_キー\_EXCHANGED します。

4.  [ *COPPSequenceStart* ](https://msdn.microsoft.com/library/windows/hardware/ff540421)ビデオ セッションを保護モードに設定します。 ドライバーがデバイス状態の定数が現在 COPP に設定することを確認する必要がありますまず\_キー\_EXCHANGED します。 ドライバーを返す必要がありますそれがないかどうか、E\_予期しません。 、戻る前に、ドライバーは、COPP にデバイスの状態の定数を設定する必要があります\_セッション\_ビデオ セッションが、保護モードを表示するのにはアクティブです。

ビデオのミニポート ドライバーが処理できるビデオ セッションを保護されたモードに設定すると後、 [COPP コマンド](copp-commands.md)の要求と[COPP 状態](copp-status.md)、渡す[COPP ステータス イベント](copp-status-events.md)。

 

 





