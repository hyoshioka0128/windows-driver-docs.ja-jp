---
title: OID_WWAN_PIN_EX2
description: OID_WWAN_PIN_EX2 は、UICC 線形固定ファイルまたは循環ファイルにアクセスします。構造型は WwanUiccFileStructureCyclic または WwanUiccFileStructureLinear です。
ms.assetid: F5D0A1B8-4D7E-469A-B738-2965D254868E
ms.date: 04/10/2019
keywords:
- Windows Vista 以降のネットワークドライバーの OID_WWAN_PIN_EX2
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 95230980572820cea51d20b39ca7872ba41de51d
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918132"
---
# <a name="oid_wwan_pin_ex2"></a>OID_WWAN_PIN_EX2

OID_WWAN_PIN_EX2 は、暗証番号 (Pin) に関連する拡張情報を設定または返します。 OID_WWAN_PIN_EX2 は[OID_WWAN_PIN_EX](oid-wwan-pin-ex.md)に似ていますが、複数アプリの uicc カードをサポートするように拡張されています。

クエリペイロードには、PIN を照会する対象アプリケーション ID を指定する[**NDIS_WWAN_PIN_APP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_app)構造が含まれます。 ミニポートドライバーは、クエリ要求を非同期的に処理し、最初に元の要求に NDIS_STATUS_INDICATION_REQUIRED を返してから、アプリケーションの PIN を記述する[**NDIS_WWAN_PIN_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)構造を含む[NDIS_STATUS_WWAN_PIN_INFO](ndis-status-wwan-pin-info.md)状態通知を送信する必要があります。 

設定ペイロードには、アプリケーションに対して実行する PIN アクションを指定する[**NDIS_WWAN_SET_PIN_EX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex2)構造が含まれます。 ミニポートドライバーは、セット要求を非同期に処理し、最初に元の要求に NDIS_STATUS_INDICATION_REQUIRED を返してから、アプリケーションの PIN の状態を記述する[**NDIS_WWAN_PIN_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)構造を含む[NDIS_STATUS_WWAN_PIN_INFO](ndis-status-wwan-pin-info.md)状態通知を送信する必要があります。

## <a name="remarks"></a>注釈

1つの検証に対応した UICCs のみがサポートされています。 複数のアプリケーション PIN をサポートするマルチ検証対応の UICCs はサポートされていません。 1つのアプリケーション PIN (PIN1) が、UICC 上のすべての ADFs/DFs およびファイルに割り当てられます。 ただし、各アプリケーションでは、レベル2のユーザー検証要件としてローカル PIN (PIN2) を指定できます。その結果、すべてのアクセスコマンドに対して追加の検証が必要になります。 このシナリオは OID_WWAN_PIN_EX2 でサポートされています。

OID_WWAN_PIN_EX2 [OID_WWAN_PIN_EX](oid-wwan-pin-ex.md)と同様に、デバイスは一度に1つの PIN のみを報告します。 複数の Pin が有効になっており、複数の Pin が有効になっている場合は、ミニポートドライバーで PIN1 を最初に報告する必要があります。 たとえば、subsidy ロックレポートが有効で、SIM の PIN1 が有効になっている場合は、 **Pinsize**をゼロ (0) に設定することによって PIN1 を指定した後にのみ、後続のクエリ要求で SUBSIDY lock PIN を報告する必要があります。 この場合、セット要求はクエリに似ており、参照先の PIN の状態を返します。 これは、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)のセクション11.1.9 で指定されている VERIFY コマンドの動作に完全に対応しています。

この OID の使用方法の詳細については、「 [MB UICC アプリケーションとファイルシステムアクセス](mb-uicc-application-and-file-system-access.md)」を参照してください。

## <a name="requirements"></a>要件

**バージョン**: Windows 10 バージョン 1903**ヘッダー**: Ntddndis (Ndis .h を含む)

## <a name="see-also"></a>こちらもご覧ください

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_PIN_INFO](ndis-status-wwan-pin-info.md)

[**NDIS_WWAN_PIN_APP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_app)

[**NDIS_WWAN_SET_PIN_EX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex2)

[**NDIS_WWAN_PIN_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)
