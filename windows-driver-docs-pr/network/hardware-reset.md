---
title: ミニポート ドライバー ハードウェア リセット
description: ミニポート ドライバー ハードウェア リセット
ms.assetid: d5209809-039c-4ac2-afdf-1f5144307850
keywords:
- ネットワーク インターフェイス カードの WDK ネットワー キング、リセット
- WDK の Nic をリセットするネットワークを
- NIC をリセットします。
- MiniportResetEx
- ハードウェアは、WDK NDIS をリセットします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 910ddf81b74e9e316d4de863609c0f1e91390d25
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342627"
---
# <a name="miniport-driver-hardware-reset"></a>ミニポート ドライバー ハードウェア リセット





ミニポート ドライバーを登録する必要があります、 [ *MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432)関数と[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)します。

*MiniportResetEx*への呼び出しでの同期または非同期で完了できます[ **NdisMResetComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563663)(次の図を参照してください)。

![ネットワーク インターフェイス カードをリセットするかを示す図](images/207-09.png)

*MiniportResetEx*する必要があります。

-   さらに割り込みを無効にします。

-   進行中のいずれかに関連付けられているデータをクリア テキストを送信します。 たとえば、バス マスター ダイレクト メモリ アクセス (DMA) デバイスのリング バッファーの送信バッファーへのポインターがクリアされます。 逆シリアル化し、接続指向のミニポート ドライバーは、NDIS を返す必要があります\_状態\_要求\_のキューに置かれた送信要求を中止します。

-   ハードウェアの状態と、ミニポート ドライバーの内部状態をリセット操作の前に存在していた状態に復元します。

ミニポート ドライバーは、マルチキャスト アドレス、パケット フィルター、タスクのオフロード設定、およびウェイク アップのパターンを除く、デバイスのハードウェアの状態を復元します。 これらの設定は、ミニポート ドライバーまたは NDIS が復元されます。 ミニポート ドライバーでブール値を返すことによってこれらの設定を復元するため担当するユーザーを決定する、 *AddressingReset*パラメーター。

ミニポート ドライバーに返された場合**FALSE**で、 *AddressingReset*パラメーター、そのマルチキャスト アドレス、パケット フィルター、タスクのオフロード設定、およびウェイク アップするパターン、ミニポート ドライバーが復元されますその。初期状態です。 ミニポート ドライバーに返された場合**TRUE**で*AddressingReset*、NDIS 呼び出しコネクションレス ミニポート ドライバーの[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数または接続指向のミニポート ドライバーの[ **MiniportCoOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff559362)次の構成設定を設定します。

-   セット要求を使用して、ネットワーク パケット フィルター [OID\_GEN\_現在\_パケット\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569575)します。

-   マルチキャスト アドレスの一覧のセット要求を通じて[OID\_802\_3\_マルチキャスト\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff569073)します。

-   タスクのオフロード カプセル化の設定のセット要求を通じて[OID\_オフロード\_カプセル化](https://msdn.microsoft.com/library/windows/hardware/ff569762)します。

-   電源管理のウェイク アップ パターンのセット要求を通じて[OID\_PNP\_追加\_WAKE\_を\_パターン](https://msdn.microsoft.com/library/windows/hardware/ff569773)します。
    **注**  以降 NDIS 6.20 が動作では、ウェイク アップのパターンをを通じて設定[OID\_PM\_追加\_WOL\_パターン](https://msdn.microsoft.com/library/windows/hardware/ff569764)ミニポート ドライバーで復元する必要があります。

     

## <a name="related-topics"></a>関連トピック


[ミニポート ドライバーのアダプターの状態](adapter-states-of-a-miniport-driver.md)

[ミニポート アダプタの状態と操作](miniport-adapter-states-and-operations.md)

[ミニポート ドライバーのリセットと Halt 関数](https://msdn.microsoft.com/library/windows/hardware/ff564064)

 

 






