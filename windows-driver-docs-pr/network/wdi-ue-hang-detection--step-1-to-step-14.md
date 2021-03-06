---
title: UE ハング検出手順 1 ~ 14
description: UE ハング検出の手順 1 ~ 14 を以下に示します。 手順は、UE ハングの検出と回復のフローの図に対応します。
ms.assetid: 0F6F9B31-27FB-44B1-8C0E-A270E8BAF295
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d342bcbe9ab7a11cf9f72aa9dcd9c894c3b327f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357101"
---
# <a name="ue-hang-detection-steps-1-14"></a>UE ハング検出:手順 1 ~ 14


UE ハング検出の手順 1 ~ 14 を以下に示します。 手順は、図に示すように対応[UE ハングアップ検出と復旧フロー](wdi-ue-hang-detection-and-recovery-flow.md)します。

この例は、OID を使用して\_設定\_電源。

1.  NDIS は、システム電源 IRP を受信または 0 に NIC のアクティブな参照を削除します。
2.  NDIS OID が生成されます\_設定\_POWER D3 WDI ドライバーにします。
3.  WDI は WDI OID、LE までを送信する前に、タスクを含む WDI コマンド (M1) のタイマーを設定します。 コマンドがタスクの場合は、タスクの追加のタイマーも設定されます。 両方のタイマーがタイムアウト、ことができますが、最大で 1 つだけがリセット回復をトリガーできます。
4.  WDI、LE を WDI コマンドを送信します。 LE の推奨事項では、アダプターの構造で WDI OID ファームウェア コマンドが、OID を完了する必要がある場合に注意してください。 ファームウェアでは、WDI OID のジョブが完了したら、LE は、OID を完了し、アダプターの構造から削除されます。 WDI に、LE に Oid がシリアル化しますので、LE に 1 つだけのスロットを保留中の WDI OID を覚えておく必要があります。 Firmware コマンドが停止した場合、LE 返せるいつでも OID 時間が、突然の削除 (突然削除のコンテキストでかまいません) 手順 17 でないより後のファームウェアが無効になっているときにします。 それ以外の場合の LE では、診断のコールバックの前後である場合、ファームウェアに関係なく、対応するジョブが完了すると WDI OID が単純に完了します。 診断後 WDI OID を覚えておく必要がある、LE 場合、は、別のスロットを覚えておくことが必要です。 ただし、診断の後に受信した oid には、LE、触れないようにカスケード ハングを避けるため、ファームウェア。
5.  LE、ファームウェアにコマンドを送信します。
6.  Firmware コマンドがタイムアウトした場合、ハングまたは時間がかかりすぎてのファームウェアことがあります。
    -   ファームウェアが単に時間がかかりすぎる、コマンド タイムアウト後に、LE は WDI コマンドを実行できます。 UE、それを適切に処理します。
    -   ファームウェアがハングしている場合、WDI コマンドはすぐに完了しません。 LE 実行する必要がある突然の削除手順 16 であるハードウェアがリセットされたときに潜在的な競合状態の特別な処理なしで完了するには、安全では、します。

7.  WDI 診断コマンドを生成する WDI タイマーが起動します。 この WDI コマンドは、LE ドライバーへの呼び出し[ *MiniportWdiAdapterHangDiagnose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose)、WDI OID ではなく。
8.  LE は、ハードウェア コントロールの登録状態、および必要に応じて、ファームウェアの完全な状態を収集します。
    -   IHV ドライバーでは、1 (kb 単位) に限定されているハードウェア レジスタのコンテンツの収集が予想され、関数の戻り値で返すことにします。 さらに、実稼働前環境で、LE も試してください IHV が事後のデバッグを十分に実行できるように、ファイルにファームウェアのコンテキストをダンプします。 スイッチは、ハードウェア レジスタ、およびファームウェア イメージの収集を制御するレジストリ キーとして実装することができます。
    -   LE も取り消し処理の現在のコマンドをマークします。 場合を避ける診断コマンド補完競合、許容可能な場合は、LE は何もこのコマンドです。
    -   保留中の次のコマンドで、UE はリセットの結果として、WDI のコマンドを送信できます。 これらは、実行中のコマンドやクリーンアップ コマンド。 診断の呼び出しの後、LE は処理にファームウェアを触れることがなく。

9.  WDI は、コントロールの登録状態を受信します。
10. 後で、LE で示されたように、WDI はハング WDI コマンドをマークします。
11. WDI を返します (完了) WDI 完了せず、NDIS コマンド。 これは安全なため、WDI ダブル バッファー NDIS コマンド。
12. WDI は呼び出しをリセットする NDIS と呼び出し[ **NdisWriteErrorLogEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiswriteerrorlogentry)で*エラー コード*の**NDIS\_エラー\_コード\_ハードウェア\_エラー** (0xc000138a)。 これは、結果、LE のモジュールの名前を持つシステム イベント ログに記録するイベント。 エラー イベント ID として自動的にポップアップ (0xc000138a | 0 xffff) – 0n5002 します。 LE は、エラー ログの書き込みにも同じエラー コードを使用する場合、データの最初の dword 値は、LE、イベントを簡単に分離するには、高ビット セット (0x80000000) を含める必要があります。 WDI は、DWORD の最初のデータを 0x00000000 に 0x7fffffff を使用します。
13. 呼び出しを返します。
14. NDIS は IRP を完了します。

この時点で後、は、NDIS は突然の削除と再私たちを列挙するバスを呼び出します。 WDI ダブル バッファー NDIS WDI コマンドが NDIS コマンドの完了に返されるを待機することはありませんするためのコマンドことに注意してください。 重要です。 これは周知のとおりを行う複雑なロジックをキャンセルする LE の必要はありません。

NDIS OID が完成したら、\_設定\_POWER PnP 操作のデッドロックを回避する必要があります。 すべての PnP と電力の状態変更イベントのシリアル化されます。 つまり、セット power OID が返さない場合、NDIS をセット power IRP が突然削除と回復のリセット ハングアップすることを意味する、IRP を返すことはできません。

## <a name="related-topics"></a>関連トピック


[*MiniportWdiAdapterHangDiagnose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_adapter_hang_diagnose)

[(突然の削除) のリセット: 15 ~ 20 のステップ](wdi-reset--surprise-remove---steps-15-20.md)

[UE ハングアップ検出と復旧フロー](wdi-ue-hang-detection-and-recovery-flow.md)

 

 






