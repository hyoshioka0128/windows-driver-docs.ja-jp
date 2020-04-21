---
title: WlanAssert rule (ndis)
description: WlanAssert 規則には、WDIWIFI ドライバー内で検証された一連のチェックが含まれています。
ms.assetid: CCA68C4D-618A-4DE4-9DEB-2A03DCD38667
ms.date: 04/08/2020
keywords:
- WlanAssert rule (ndis)
topic_type:
- apiref
api_name:
- WlanAssert
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 158a0752bedbe9f6b339270aa9bb131a93aa7ac3
ms.sourcegitcommit: 84be9e06fd0886598df77dffcbc75632d613c8f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219516"
---
# <a name="wlanassert-rule-ndis"></a>WlanAssert rule (ndis)

**WlanAssert**規則には、WDIWIFI ドライバー内で検証された一連のチェックが含まれています。

次の違反が発生する可能性があります。

- *Txpeerbacklogstub: データパス deinitialization の後にデータパスという名前の IHV WDI ミニポート*が適用されます。このルールはピアキューモードにのみ適用されます。 ミニポートが停止またはリセットされると、WDI は IHV ドライバーの[Closeadapterhandler](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_close_adapter)関数を呼び出します。この関数では、ドライバーの状態をクリーンアップする必要があり、その後のデータコールバックは呼び出されません。 これらのアサートは、ドライバーが[Txtransfercompleteindication](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_transfer_complete_ind)、 [TxSendPauseIndication](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_pause_ind)、または終了後に、 [txreleaseframes](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_release_frames_ind)などのデータハンドラーを呼び出す場合、またはクローズ後に未処理の Tx フレームが残っている場合に呼び出されます。

- *Txabortstub: IHV WDI ミニポートは、データパス deinitialization 後にデータパスと呼ばれ*ます。このルールはピアキューモードにのみ適用されます。 ミニポートが停止またはリセットされると、WDI は IHV ドライバーの[Closeadapterhandler](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_close_adapter)関数を呼び出します。この関数では、ドライバーの状態をクリーンアップする必要があり、その後のデータコールバックは呼び出されません。 これらのアサートは、ドライバーが[Txtransfercompleteindication](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_transfer_complete_ind)、 [TxSendPauseIndication](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_pause_ind)、または終了後に、 [txreleaseframes](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_release_frames_ind)などのデータハンドラーを呼び出す場合、またはクローズ後に未処理の Tx フレームが残っている場合に呼び出されます。

- *WDIWIFI ドライバーは、NdisMDeregisterWdiMiniportDriver と NdisMRegisterWdiMiniportDriver の呼び出しが一致しない状態でアンロードされ*ます。この Assert は、ihv ドライバーの[NdisMRegisterWdiMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver)への呼び出しが失敗した場合に呼び出されますが、Ihv ドライバーは引き続き[NdisMDeregisterWdiMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismderegisterwdiminiportdriver)ハンドラーを呼び出します。

- *IhvWdiVersion は渡された MiniportDataHandler リビジョンに対して低すぎるため*、WDI は[OID_WDI_GET_ADAPTER_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)を呼び出して IHV ドライバーの WDI バージョンを取得し、ドライバーの[TalTxRxInitializeHandler](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tal_txrx_initialize)ハンドラーを呼び出して[WdiCharacteristics](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)を取得します。この場合、ドライバーは必要に応じて WDI handler のリビジョンを更新できます。 ドライバーの WDI バージョンが WDI_VERSION_1_1_0 以下で、ドライバーの[WdiCharacteristics](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)、Revision が NDIS_OBJECT_TYPE_MINIPORT_WDI_DATA_HANDLERS_REVISION_1 よりも大きいバージョンに設定されている場合、このアサーションはヒットします。

- *MiniportDataHandler のリビジョンが低すぎる*と、WDI は[OID_WDI_GET_ADAPTER_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)を呼び出して IHV ドライバーの WDI バージョンを取得し、ドライバーの[TalTxRxInitializeHandler](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tal_txrx_initialize)ハンドラーを呼び出して[WdiCharacteristics](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)を取得します。この場合、ドライバーは必要に応じて WDI handler のリビジョンを更新できます。 ドライバーの WDI のバージョンが WDI_VERSION_1_1_0 よりも大きくても、ドライバーの[WdiCharacteristics](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)、Revision が NDIS_OBJECT_TYPE_MINIPORT_WDI_DATA_HANDLERS_REVISION_2 よりも小さいバージョンに設定されている場合、このアサーションはヒットします。

0xC4 バグチェックでは、*違反テキスト*がパラメーター2として指定されます。

|              |      |
|--------------|------|
| ドライバー モデル | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| この規則で見つかったバグ チェック | [**バグチェック 0xc4: ドライバー\_VERIFIER\_検出され\_違反**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)が発生しました (0x00093004) |

<a name="how-to-test"></a>テスト方法
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">実行時</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)">ドライバーの検証ツール</a>を実行し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification" data-raw-source="[NDIS/WIFI verification](https://docs.microsoft.com/windows-hardware/drivers/devtest/ndis-wifi-verification)">NDIS/WIFI 検証</a>オプションを選択します。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>状態名
----------

[TxTransferCompleteIndication](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_transfer_complete_ind)

[TxSendPauseIndication](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_pause_ind)

[Txreleaseフレームの表示](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_release_frames_ind) 

[OID_WDI_GET_ADAPTER_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)

[MINIPORT_HALT コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)

[MINIPORT_SHUTDOWN コールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)

[NdisMRegisterWdiMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver)

[NdisMDeregisterWdiMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismderegisterwdiminiportdriver)

<a name="see-also"></a>参照
--------

[WDI IHV ドライバーインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-ihv-driver-interfaces)

[一般的な接続操作のガイドライン](https://docs.microsoft.com/windows-hardware/drivers/network/general-connection-operation-guidelines)

[OID\_DOT11\_リセット\_要求](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-reset-request)

[NDIS\_STATUS\_DOT11\_アソシエーション\_開始](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-association-start)
