---
title: OID_WWAN_PIN_EX2
description: OID_WWAN_PIN_EX2 は UICC 線形固定または循環がファイルを構造型の WwanUiccFileStructureCyclic または WwanUiccFileStructureLinear にアクセスします。
ms.assetid: F5D0A1B8-4D7E-469A-B738-2965D254868E
ms.date: 04/10/2019
keywords:
- OID_WWAN_PIN_EX2 ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 126f8a38903e477bffe60b07086d038050518124
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354579"
---
# <a name="oidwwanpinex2"></a>OID_WWAN_PIN_EX2

OID_WWAN_PIN_EX2 を設定または暗証番号 (Pin) に関連する拡張情報を取得します。 OID_WWAN_PIN_EX2 と似ています[OID_WWAN_PIN_EX](oid-wwan-pin-ex.md)がマルチ アプリ UICC カードをサポートするように拡張します。

クエリのペイロードを含む、 [ **NDIS_WWAN_PIN_APP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_app)照会される対象アプリケーション ID の暗証番号 (pin) を指定する構造体。 ミニポート ドライバーが非同期的に、最初に、元の要求に NDIS_STATUS_INDICATION_REQUIRED を返すこと、後で送信する前にクエリ要求を処理する必要があります、 [NDIS_STATUS_WWAN_PIN_INFO](ndis-status-wwan-pin-info.md)状態通知を含む[ **NDIS_WWAN_PIN_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)アプリケーションの暗証番号 (pin) を記述する構造体。 

セットのペイロードを含む、 [ **NDIS_WWAN_SET_PIN_EX2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex2)アプリケーションを実行するピン留めするアクションを指定する構造体。 ミニポート ドライバーする必要がありますセット要求を非同期に処理、最初に NDIS_STATUS_INDICATION_REQUIRED を後で送信する前に、元の要求を返す、 [NDIS_STATUS_WWAN_PIN_INFO](ndis-status-wwan-pin-info.md)状態通知を含む、[ **NDIS_WWAN_PIN_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)アプリケーションの暗証番号 (pin) の状態を記述する構造体。

## <a name="remarks"></a>注釈

1 つの検証に対応した UICCs のみがサポートされています。 暗証番号 (pin) がサポートされていない 1 つ以上のアプリケーションをサポートするマルチ verification 対応 UICCs します。 1 つのアプリケーション (PIN1) 暗証番号 (pin) は、すべての ADFs/DFs と、UICC 上のファイルに割り当てられます。 ただし、各アプリケーションでは、すべてのアクセス コマンドの追加の検証が必要になり、レベル 2 のユーザーの検証要件として、ローカルの PIN (暗証番号 2) を指定できます。 このシナリオは、OID_WWAN_PIN_EX2 がサポートしています。

同じように[OID_WWAN_PIN_EX](oid-wwan-pin-ex.md)OID_WWAN_PIN_EX2 でデバイスを報告するだけ 1 つの PIN、時にします。 複数の Pin が有効になっているし、複数の Pin の報告を有効に、ミニポート ドライバーする必要がありますを報告 PIN1 最初。 たとえば、subsidy ロックの報告を有効にすると、SIM の PIN1 が有効になっている、し subsidy ロック PIN に報告されます後続のクエリ要求 PIN1 指定を設定した後にのみ、 **PinSize**をゼロ (0)。 ここでは、セットの要求は、クエリに似ていますし、参照されている PIN の状態を返します。 指定したセクション 11.1.9 の確認 コマンドの動作に整列されて完全、 [ETSI TS 102 221 技術仕様](https://go.microsoft.com/fwlink/p/?linkid=864594)します。

この OID の使用状況に関する詳細については、次を参照してください。 [MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)します。

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| バージョン | Windows 10 バージョン 1903 |
| Header | Ntddndis.h (include Ndis.h) |

## <a name="see-also"></a>関連項目

[MB UICC アプリケーションとファイル システム アクセス](mb-uicc-application-and-file-system-access.md)

[NDIS_STATUS_WWAN_PIN_INFO](ndis-status-wwan-pin-info.md)

[**NDIS_WWAN_PIN_APP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_app)

[**NDIS_WWAN_SET_PIN_EX2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin_ex2)

[**NDIS_WWAN_PIN_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)
