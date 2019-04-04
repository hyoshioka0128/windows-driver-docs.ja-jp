---
title: ミニポート アダプターの Check-for-Hang 操作とリセット操作
description: ミニポート アダプターの Check-for-Hang 操作とリセット操作
ms.assetid: 53ffc5a9-bcba-4189-8845-73adfcf6816d
keywords:
- ミニポート アダプタ WDK、ネットワークのチェック-ハングの操作
- ミニポート アダプタの WDK ネットワー キング、リセットの操作
- アダプター WDK、ネットワークのチェック-ハングの操作
- アダプターの WDK ネットワー キング、リセットの操作
- MiniportCheckForHangEx
- ハングし、o をリセット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab54d733f705f88d83236b54f95e319bff288635
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573817"
---
# <a name="miniport-adapter-check-for-hang-and-reset-operations"></a>ミニポート アダプターの Check-for-Hang 操作とリセット操作

## <a name="overview"></a>概要

> [!WARNING]
> すべての NDIS 6.83 およびそれ以降のドライバーは、チェックのハング (CFH) とリセットの操作は推奨されません。 詳細については、[NDIS 6.83 以降のチェック-ハング用とリセット操作](#check-for-hang-and-reset-operations-in-ndis-683-and-later)を参照してください。

NDIS 呼び出し NDIS ミニポート ドライバーの[ *MiniportCheckForHangEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559346)ネットワーク インターフェイス カード (NIC) を表す NDIS アダプターの操作の状態を確認する関数。 *MiniportCheckForHangEx*アダプターの内部状態をチェックし、返します**TRUE**アダプターが正しく動作しないことを検出した場合。

既定では、NDIS を呼び出す*MiniportCheckForHangEx*約 2 秒間隔。 場合*MiniportCheckForHangEx*返します**TRUE**、NDIS 呼び出し、NDIS ミニポート ドライバーの[ *MiniportResetEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559432)関数。 2 秒の既定のタイムアウト値が小さすぎる場合、ミニポート ドライバーできますように設定を別の値の初期化時。

1.  設定、 **CheckForHangTimeInSeconds**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934) 0 以外の値構造体。
2.  渡す、 [ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)構造体、 *MiniportAttributes*のパラメーター、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数。

ドライバー属性の設定の詳細については、[、アダプターの初期化](initializing-a-miniport-adapter.md)を参照してください。
値**CheckForHangTimeInSeconds**ミニポート ドライバーの初期化時間よりも大きい必要があります。 ただし、ドライバーがより長くかかる場合**CheckForHangTimeInSeconds**秒を初期化するこのタイムアウトになるを呼び出してドライバーの ndis *MiniportCheckForHangEx*関数。 場合*MiniportCheckForHangEx*返します**TRUE**、NDIS を呼び出し、ドライバーの*MiniportResetEx*関数。 このため、ドライバーを同期する必要があります[ *MiniportCheckForHangEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559346)ドライバーの初期化で動作する*MiniportCheckForHangEx*されません返す**TRUE**ドライバーが初期化を完了していない場合。

ミニポート ドライバーに 2 つの連続呼び出し内の OID 要求は、完了しない場合*MiniportCheckForHangEx*、NDIS ドライバーを呼び出すことができます*MiniportResetEx*関数。 一部の OID 要求では、NDIS 呼び出し*MiniportResetEx*ドライバーでは 4 つの連続呼び出し内での要求が完了しないかどうか*MiniportCheckForHangEx*します。

リセット操作には影響しません[ミニポート アダプタの操作状態](miniport-adapter-states-and-operations.md)します。 また、リセット操作が進行中は、アダプターの状態を変更する可能性があります。 NDIS ドライバーの呼び出すものなど[ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418)進行中のリセット操作がある場合に機能します。 この場合、ドライバーは、リセット、または要件は、各操作の実行中に任意の順序で一時停止操作を完了できます。

ドライバーが要求パケットの送信の失敗時に、リセット操作またはキューに置かれ、完全に保持できる後でもです。 上位のドライバーが中に一時停止操作を完了できないことを確認する必要がありますただし、その送信パケットが保留中です。

ミニポート ドライバーでは、成功または失敗の状態を返すことによって、リセット要求を同期的に完了できます。 ドライバーを返すことによってリセット要求を非同期的に実行できる**NDIS\_状態\_PENDING**します。 この場合、ドライバーを呼び出す必要があります[ **NdisMResetComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563663)操作を完了します。

## <a name="check-for-hang-and-reset-operations-in-ndis-683-and-later"></a>チェックのハングのおよび NDIS 6.83 以降のリセット操作

6.83 前に、のバージョンの NDIS チェックのハング (CFH) とのリセット操作が常に、常に Connected (AOAC) システムでバッテリ寿命の問題のための推奨されません。 ただし、ドライバーでした使用 CFH AOAC 以外の Windows の他のシステムで、省略可能な実装することによって[ *MiniportCheckForHangEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_check_for_hang)と[ *MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)コールバック関数。 

NDIS 6.83 以降、これらのコールバック関数は推奨されませんで**すべて**電源機能に関係なく、Windows システムです。 CFH NDIS 6.83 以降を使用するロゴ テスト違反ではありませんが、NDIS ドライバーは、その使用法についてのガイダンスについては、次の表を使用してください。

| 呼び出し元 | 推奨 | メモ |
| --- | --- | --- |
| ドライバーの AOAC システムを対象とします。 | 実装する必要があります。 | 定期的なチェックのハングのアクティビティのためのバッテリ寿命の問題が発生します。 |
| Windows Server システムを対象とするドライバー | 実装する必要があります。 | CPU に負荷がかかっているときに問題が発生します。 |
| 仮想 (ソフトウェア専用) のミニポート ドライバー | 実装する必要があります。 | リセットできないハードウェアなし |
| 他の新しい NDIS 6.83 およびそれ以降のドライバー | 実装しないでください。 |
| その他の既存の NDIS 6.82 と以前のコード | 変更するには必要ありませんが、削除のチェック-ハングのおよびリセットが後で再作成を検討してください |

## <a name="related-topics"></a>関連トピック


[ミニポート ドライバーのハードウェアのリセット](hardware-reset.md)

[ミニポート ドライバーのリセットと Halt 関数](https://msdn.microsoft.com/library/windows/hardware/ff564064)

 

 






