---
title: 仮想ミニポートの初期化
description: 仮想ミニポートの初期化
ms.assetid: b712fe29-fd56-4abd-bab6-e335350a20c2
keywords:
- 基になるアダプターの WDK ネットワークを開く
- アダプターを基になるを開く
- 仮想ミニポート WDK ネットワーク
- 初期化中の仮想ミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1e964df868337f520cd460caf90b5648c55b440
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324933"
---
# <a name="initializing-virtual-miniports"></a>仮想ミニポートの初期化





中間のドライバーは、基になるミニポート アダプターが正常に開かれてと要求を受け入れる準備が整うし、その仮想ミニポートに送信した後、その仮想 miniports を初期化します。 中間のドライバーは呼び出し[ **NdisIMInitializeDeviceInstanceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff562727)からその[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220) 1 つまたは複数の関数1 つまたは複数の仮想ミニポートの初期化を要求する回数。

**注**  中間のドライバーを呼び出す必要はありません**NdisIMInitializeDeviceInstanceEx**基になるミニポート アダプターを開いたとき。 存在する必要はありません仮想ミニポートと開いているアダプターの一対一の関係があります。

 

設定、 *DriverInstance*パラメーターの**NdisIMInitializeDeviceInstanceEx**仮想ミニポートの初期化中のデバイス名にします。 中間ドライバーからデバイス名の取得、 **UpperBindings**レジストリ キー。

*N*-を-1 つのマルチプレクサー中間レイヤーを 1 つの物理 NIC に複数の仮想ミニポート ドライバー、すべて仮想ミニポートのデバイス名が必要があります。 MUX 中間ドライバーには、仮想ミニポート デバイス名の一覧を保持する通知オブジェクトが必要です。 一覧については、推奨される場所は、 **UpperBindings**レジストリ キー。 ここで、 **UpperBindings**レジストリ キーは、マルチ\_デバイス名の一覧を含む SZ エントリ。 MUX 中間ドライバー呼び出し**NdisIMInitializeDeviceInstanceEx**デバイス名の一覧で指定されているデバイス名ごとに 1 回です。

呼び出す**NdisIMInitializeDeviceInstanceEx**中間ドライバーの呼び出しで結果[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)の初期化を実行する関数、NDIS IRP を受信することは、仮想のミニポートを指定した\_MN\_開始\_デバイスのデバイスを起動します。 NDIS 中間ドライバは呼び出しません NDIS がこのような IRP を受信しない場合*MiniportInitializeEx*関数。 呼び出し*MiniportInitializeEx*は後で発生することができます、そのため必ずしもへの呼び出しのコンテキスト内で**NdisIMInitializeDeviceInstanceEx**します。 NDIS は呼び出すことはない場合*MiniportInitializeEx*への呼び出しで参照されている仮想ミニポートの**NdisIMInitializeDeviceInstanceEx**、中間のドライバーが仮想のミニポートを不要と中間のドライバーを呼び出す必要があります[ **NdisIMCancelInitializeDeviceInstance** ](https://msdn.microsoft.com/library/windows/hardware/ff562719)仮想ミニポートの初期化をキャンセルします。 たとえば、中間のドライバーが、基になるミニポートへのバインドを成功への応答で仮想ミニポートを作成します。 NDIS 呼び出される前にそのバインドが削除された場合*MiniportInitializeEx*、中間のドライバーを呼び出す必要があります**NdisIMCancelInitializeDeviceInstance**ミニポートの初期化をキャンセルします。

*MiniportInitializeEx*割り当ておよび仮想ミニポートに固有のコンテキストの領域を初期化する必要があります。 コンテキストの領域を指定する方法については、次を参照してください。[初期化仮想ミニポート](initializing-a-virtual-miniport.md)します。

中間のドライバーは、逆シリアル化されたドライバーとして機能する必要があります。 逆シリアル化されたドライバーの詳細については、次を参照してください。 [NDIS ミニポート ドライバーの逆シリアル化](deserialized-ndis-miniport-drivers.md)します。

中間のドライバーでは、状態情報を保持が正しく初期化されているを確認してください。 たとえば、新しいドライバーに送信に関連するリソースが必要な場合[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)ネットワーク データの構造を[ *MiniportSendNetBufferLists* ](https://msdn.microsoft.com/library/windows/hardware/ff559440)は [次へ] の下位の層 - NET に送信する\_バッファー\_リスト構造プールこの時点で割り当てることができます。

 

 





