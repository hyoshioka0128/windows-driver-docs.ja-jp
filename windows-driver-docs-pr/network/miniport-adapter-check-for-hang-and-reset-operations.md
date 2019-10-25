---
title: ミニポート アダプターの Check-for-Hang 操作とリセット操作
description: ミニポート アダプターの Check-for-Hang 操作とリセット操作
ms.assetid: 53ffc5a9-bcba-4189-8845-73adfcf6816d
keywords:
- ミニポートアダプター WDK ネットワーク、ハングチェック操作
- ミニポートアダプター WDK ネットワーク、リセット操作
- WDK ネットワークのアダプター、ハングチェック操作
- WDK ネットワークのアダプタ、リセット操作
- MiniportCheckForHangEx
- ハングしてリセット o
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 411396de557625c94f2281377a8e5626aa2597b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844257"
---
# <a name="miniport-adapter-check-for-hang-and-reset-operations"></a>ミニポート アダプターの Check-for-Hang 操作とリセット操作

## <a name="overview"></a>概要

> [!WARNING]
> すべての NDIS 6.83 以降のドライバーでは、チェック-ハング (CFH) とリセット操作を使用しないことをお勧めします。 詳細については、「 [Check To Hang And Reset operation IN NDIS 6.83](#check-for-hang-and-reset-operations-in-ndis-683-and-later)」を参照してください。

NDIS は、ndis ミニポートドライバーの[*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang)関数を呼び出して、ネットワークインターフェイスカード (NIC) を表す ndis アダプターの動作状態を確認します。 *MiniportCheckForHangEx*は、アダプターの内部状態を確認し、アダプターが正常に動作していないことを検出した場合は**TRUE**を返します。

既定では、NDIS は約2秒ごとに*MiniportCheckForHangEx*を呼び出します。 *MiniportCheckForHangEx*が**TRUE**を返す場合、ndis は ndis ミニポートドライバーの[*miniportresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)関数を呼び出します。 既定のタイムアウト値2秒が小さすぎる場合は、次のように、ミニポートドライバーで初期化時に別の値を設定できます。

1.  [**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)構造の**CheckForHangTimeInSeconds**メンバーを0以外の値に設定します。
2.  [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)関数の*miniportattributes*パラメーターに、 [**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)の構造を渡します。

ドライバー属性の設定の詳細については、「[アダプターの初期化](initializing-a-miniport-adapter.md)」を参照してください。
**CheckForHangTimeInSeconds**の値は、ミニポートドライバーの初期化時間よりも大きくする必要があります。 ただし、ドライバーの初期化に**CheckForHangTimeInSeconds**秒以上かかる場合、このタイムアウトは期限切れになり、NDIS によってドライバーの*MiniportCheckForHangEx*関数が呼び出されます。 *MiniportCheckForHangEx*が**TRUE**を返す場合、NDIS はドライバーの*miniportresetex*関数を呼び出します。 このため、ドライバーの初期化が完了していない場合、 *MiniportCheckForHangEx*が**TRUE**を返さないように、ドライバーの[*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang)関数をドライバーの初期化と同期する必要があります。

ミニポートドライバーが、 *MiniportCheckForHangEx*の2回目の呼び出し内で OID 要求を完了しない場合、NDIS はドライバーの*Miniportresetex*関数を呼び出すことができます。 一部の OID 要求では、 *MiniportCheckForHangEx*への連続した4回の呼び出し内でドライバーが要求を完了しない場合、NDIS は*Miniportresetex*を呼び出します。

リセット操作は、[ミニポートアダプターの動作状態](miniport-adapter-states-and-operations.md)に影響しません。 また、リセット操作の実行中にアダプターの状態が変わる可能性があります。 たとえば、NDIS は、実行中のリセット操作があるときに、ドライバーの[*Miniportpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)関数を呼び出す場合があります。 この場合、ドライバーは、各操作の通常の要件に従って、任意の順序でリセット操作または一時停止操作を完了できます。

リセット操作の場合、ドライバーは要求パケットの送信に失敗することがあります。または、キューをキューに入れて後で完了させることができます。 ただし、送信パケットが保留されている間は、後続のドライバーが一時停止操作を完了できないことに注意してください。

ミニポートドライバーは、成功または失敗の状態を返すことによって、リセット要求を同期的に完了させることができます。 ドライバーは、 **NDIS\_STATUS\_PENDING**を返すことによって、リセット要求を非同期に完了できます。 この場合、ドライバーは[**NdisMResetComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismresetcomplete)を呼び出して操作を完了する必要があります。

## <a name="check-for-hang-and-reset-operations-in-ndis-683-and-later"></a>NDIS 6.83 以降のハングおよびリセット操作の確認

6\.83 より前のバージョンの NDIS では、バッテリの寿命に問題があるため、Always On、常に接続されている (または電源に接続されている) システムでは、チェック-ハング (CFH) とリセット操作を使用しないことをお勧めしました。 ただし、ドライバーは、オプションの[*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang)および[*Miniportresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)コールバック関数を実装することで、他の非機能の ac Windows システムでも cfh を使用できます。 

NDIS 6.83 以降、これらのコールバック関数は、電源機能に関係なく、**すべて**の Windows システムで推奨されません。 NDIS 6.83 以降で CFH を使用するためのロゴテスト違反ではありませんが、NDIS ドライバーでは、その使用方法に関するガイダンスとして次の表を使用する必要があります。

| コール | 推奨事項 | 注意 |
| --- | --- | --- |
| 交流システムを対象とするドライバー | 実装しない | 定期的なハングチェックのアクティビティによって、バッテリの寿命に関する問題を発生させます。 |
| Windows Server システムを対象とするドライバー | 実装しない | CPU の負荷が発生したときに問題が発生します。 |
| 仮想 (ソフトウェアのみ) ミニポートドライバー | 実装しない | ハードウェアがないとリセットできません |
| その他の新しい NDIS 6.83 以降のドライバー | 実装しない |
| その他の既存の NDIS 6.82 およびそれ以前のコード | 変更する必要はありませんが、今後の作業のために、停止時のチェックを削除してリセットすることを検討してください |

## <a name="related-topics"></a>関連トピック


[ミニポートドライバーのハードウェアリセット](hardware-reset.md)

[ミニポートドライバーのリセットと停止の機能](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff564064(v=vs.85))

 

 






