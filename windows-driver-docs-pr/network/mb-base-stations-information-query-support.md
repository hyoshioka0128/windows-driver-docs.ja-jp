---
title: MB ベース ステーション情報クエリのサポート
description: MB ベース ステーション情報クエリのサポート
ms.assetid: 200954a6-0f6c-4c00-86cb-510399f7b713
keywords:
- MB のベースに情報の照会、モバイル ブロード バンド ベース ステーション情報の照会
ms.date: 08/14/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40fe784a7da6f45573c2ca3f7f0fcd0074b2e46e
ms.sourcegitcommit: ba351c01be491b8ab5c74d778ab02c8766a5667a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "67041366"
---
# <a name="mb-base-stations-information-query-support"></a>MB ベース ステーション情報クエリのサポート

## <a name="overview"></a>概要

携帯電話の基地局の情報になど場所ベースのサービスを提供する基地局情報のクエリ インターフェイスが使用される*ベース ステーション ID*、*時間事前*、そのことができる他のパラメーターモバイルのサブスクライバーの地理的位置の計算に使用します。 収集した情報は、現在のサブスクライバーを提供しているだけでなく携帯電話の基地局の隣接する携帯電話基地局に関連します。 

MBIM 1.0 の仕様は、既存の Cid を通じてこの情報を指定しないために、このトピックでは、Windows の基地局情報のクエリ インターフェイスを定義します。 このインターフェイスは、Windows 10 バージョン 1709 以降で使用できます。 

サービスを提供し、近隣のセルのパラメーターは、クエリ/応答操作を通じて取得されます。 通知は、移動体通信ネットワーク内のデバイスの場所が変更されたことを示すには、このトピックでも定義されています。

## <a name="mbim_cid_base_stations_info"></a>MBIM_CID_BASE_STATIONS_INFO

このコマンドでは、モデムに既知のサービスを提供し、近隣のセルに関する情報を取得します。

サービス:**MBB_UUID_BASIC_CONNECT_EXTENSIONS**

サービス UUID:**3d01dcc5-fef5-4d05-0d3a-bef7058e9aaf**

| CID | コマンド コード | 最小 OS バージョン |
| --- | --- | --- |
| MBIM_CID_BASE_STATIONS_INFO | 11 | Windows 10 バージョン 1709 |

### <a name="parameters"></a>パラメーター

| | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | MBIM_BASE_STATIONS_INFO_REQ | 該当なし |
| 応答 | Appliable されません。 | MBIM_BASE_STATIONS_INFO | 該当なし |

### <a name="query"></a>クエリ

MBIM_COMMAND_MSG InformationBuffer にはには、MBIM_BASE_STATIONS_INFO_REQ 構造が含まれています。 MBIM_COMMAND_DONE InformationBuffer には MBIM_BASE_STATIONS_INFO 構造体が含まれています。

#### <a name="mbim_base_stations_info_req"></a>MBIM_BASE_STATIONS_INFO_REQ

MBIM_BASE_STATIONS_INFO_REQ 構造体は、クエリの InformationBuffer で使用されます。 セルについては、応答で送信する近隣セル単位の最大数などの側面を構成に使用されます。 

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | MaxGSMCount | サイズ | GSM の隣接するセルのエントリの最大数は、の GSM ネットワーク測定レポートで返される[MBIM_GSM_NMR](#mbim_gsm_nmr)します。 既定の容量は、15 です。 |
| 4 | 4 | MaxUMTSCount | サイズ | UMTS 測定結果リストで UMTS 隣接するセルのエントリの最大数が返される[MBIM_UMTS_MRL](#mbim_umts_mrl)します。 既定の容量は、15 です。 |
| 8 | 4 | MaxTDSCDMACount | サイズ | TDSCDMA 測定結果リストで TDSCDMA 隣接するセルのエントリの最大数が返される[MBIM_TDSCDMA_MRL](#mbim_tdscdma_mrl)します。 既定の容量は、15 です。 |
| 12 | 4 | MaxLTECount | サイズ | 測定 LTE 結果一覧の隣接するセル LTE のエントリの最大数が返される[MBIM_LTE_MRL](#mbim_lte_mrl)します。 既定の容量は、15 です。 |
| 16 | 4 | MaxCDMACount | サイズ | CDMA 測定結果リストで CDMA セルのエントリの最大数が返される[MBIM_CDMA_MRL](#mbim_cdma_mrl)します。 この一覧には、サービスを提供して、隣接するセルが含まれています。 既定の容量には 12 です。 |

### <a name="set"></a>Set

適用できません。

### <a name="response"></a>応答

MBIM_BASE_STATIONS_INFO 構造体は、応答の MBIM_COMMAND_DONE InformationBuffer ので使用されます。

#### <a name="mbim_base_stations_info"></a>MBIM_BASE_STATIONS_INFO

MBIM_BASE_STATIONS_INFO 構造体には、提供していると、隣接する基地局両方に関する情報が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SystemType | MBIM_DATA_CLASS | セルの情報が有効にするサービスのシステムの種類 (または型) を示します。 このメンバーは、1 つまたは複数のシステム型、MBIM_DATA_CLASS で定義されているのビットマスクです。 |
| 4 | 4 | GSMServingCellOffset | OFFSET | セルの情報を提供している、GSM を保持するバッファーをこの構造体の先頭からのオフセット (バイト単位) が計算されます。 このメンバーは、サービスのセルのテクノロジは GSM ではない場合、NULL にすることができます。 |
| 8 | 4 | GSMServingCellSize | SIZE(0-44) | バイト単位の使用のサイズ、 [MBIM_GSM_SERVING_CELL_INFO](#mbim_gsm_serving_cell_info)します。 |
| 12 | 4 | UMTSServingCellOffset | OFFSET | セルの情報を提供している UMTS を格納しているバッファーに、この構造体の先頭からのオフセット (バイト単位) が計算されます。 このメンバーは、セルのサービスを提供するテクノロジは UMTS ではない場合、NULL にすることができます。 |
| 16 | 4 | UMTSServingCellSize | SIZE(0-60) | バイト単位の使用のサイズ、 [MBIM_UMTS_SERVING_CELL_INFO](#mbim_umts_serving_cell_info)します。 |
| 20 | 4 | TDSCDMAServingCellOffset | OFFSET | セルの情報を提供している TDSCDMA を格納しているバッファーに、この構造体の先頭からのオフセット (バイト単位) が計算されます。 このメンバーは、セルのサービスを提供するテクノロジは TDSCDMA ではない場合、NULL にすることができます。 |
| 24 | 4 | TDSCDMAServingCellSize | SIZE(0-48) | バイト単位の使用のサイズ、 [MBIM_TDSCDMA_SERVING_CELL_INFO](#mbim_tdscdma_serving_cell_info)します。 |
| 28 | 4 | LTEServingCellOffset | OFFSET | セルの情報を提供している LTE を格納しているバッファーに、この構造体の先頭からのオフセット (バイト単位) が計算されます。 このメンバーは、セルのサービスを提供するテクノロジは LTE ではない場合、NULL にすることができます。 |
| 32 | 4 | LTEServingCellSize | SIZE(0-48) | バイト単位の使用のサイズ、 [MBIM_LTE_SERVING_CELL_INFO](#mbim_lte_serving_cell_info)します。 |
| 36 | 4 | GSMNmrOffset | OFFSET | GSM ネットワーク測定レポートを含んでいるバッファーに、この構造体の先頭からのオフセット (バイト単位) が計算されます。 このメンバーは、測定レポートに GSM の隣接するネットワークが返されない場合、NULL にすることができます。 |
| 40 | 4 | GSMNmrSize | サイズ | GSM ネットワーク測定レポートの形式を含んでいるバッファーのバイト単位の合計サイズ[MBIM_GSM_NMR](#mbim_gsm_nmr)します。 |
| 44 | 4 | UMTSMrlOffset | OFFSET | オフセット (バイト単位) が、この構造体の先頭から計算されたバッファーに UMTS を格納している測定結果の一覧。 このメンバーは、測定レポートに UMTS 隣接するネットワークが返されない場合、NULL にすることができます。 |
| 48 | 4 | UMTSMrlSize | サイズ | UMTS を格納するバッファーのバイト単位の合計サイズの測定結果一覧の形式で[MBIM_UMTS_MRL](#mbim_umts_mrl)します。 |
| 52 | 4 | TDSCDMAMrlOffset | OFFSET | オフセット (バイト単位) が、この構造体の先頭から計算されたバッファーに TDSCDMA を格納している測定結果の一覧。 このメンバーは、測定レポートに TDSCDMA 隣接するネットワークが返されない場合、NULL にすることができます。 |
| 56 | 4 | TDSCDMAMrlSize | サイズ | TDSCDMA を格納するバッファーのバイト単位の合計サイズの測定結果一覧の形式で[MBIM_TDSCDMA_MRL](#mbim_tdscdma_mrl)します。 |
| 60 | 4 | LTEMrlOffset | OFFSET | オフセット (バイト単位) が、この構造体の先頭から計算されたバッファーに、LTE を格納している測定結果の一覧。 このメンバーは、測定レポートに LTE 隣接するネットワークが返されない場合、NULL にすることができます。 |
| 64 | 4 | LTEMrlSize | サイズ | LTE を格納するバッファーのバイト単位の合計サイズの測定結果一覧の形式で[MBIM_LTE_MRL](#mbim_lte_mrl)します。 |
| 68 | 4 | CDMAMrlOffset | OFFSET | オフセット (バイト単位) が、この構造体の先頭から計算されたバッファーに CDMA を格納している測定結果の一覧。 このメンバーは、測定レポートに CDMA 隣接するネットワークが返されない場合、NULL にすることができます。 |
| 72 | 4 | CDMAMrlSize | サイズ | CDMA を格納するバッファーのバイト単位の合計サイズの測定結果一覧の形式で[MBIM_CDMA_MRL](#mbim_cdma_mrl)します。 |
| 76 |   | DataBuffer | DATABUFFER | データ バッファーを含む*GSMServingCell*、 *UMTSServingCell*、 *TDSCDMAServingCell*、 *LTEServingCell*、 *GSMNmr*、 *UMTSMrl*、 *TDSCDMAMrl*、 *LTEMrl*、および*CDMAMrl*します。 |

#### <a name="gsm-cell-data-structures"></a>GSM セルのデータ構造体

##### <a name="mbim_gsm_serving_cell_info"></a>MBIM_GSM_SERVING_CELL_INFO

MBIM_GSM_SERVING_CELL_INFO 構造体には、GSM サービス セルに関する情報が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 呼ばれる数値 (0 ~ 9) の文字列に、この構造体の先頭からのオフセット (バイト単位) が計算される*ProviderId*プロバイダーのネットワーク id を表します。 この文字列は、3 桁 Mobile 国コード (MCC) と、2 つの連結または 3 桁モバイル ネットワーク コード mnc (も)。 このメンバーがない場合は NULL を指定できます*ProviderId*情報が返されます。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 使用サイズ*ProviderId*します。 |
| 8 | 4 | LocationAreaCode | UINT32 | 場所の市外局番 (0 ~ 65535)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 12 | 4 | CellID | UINT32 | セルの ID (0 ~ 65535) です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 16 | 4 | TimingAdvance | UINT32 | ビット期間が 48/13µs は、ビット期間でタイミング詳細 (0 ~ 255)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 20 | 4 | ARFCN | UINT32 | サービスのセル (0 ~ 1023) の絶対数の無線周波数チャネル。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 24 | 4 | BaseStationId | UINT32 | ベース ステーション ID - 基地局のカラー コードと、ネットワーク id コード。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 28 | 4 | RxLevel | UINT32 | セル (0 ~ 63) の場所、サービスの受信信号強度 <p>`X = 0, if RSS < -110 dBm`</p><p>`X = 63, if RSS > -47 dBm`</p><p>`X = integer [RSS + 110], if -110 <= RSS <= -47`</p> この情報が利用できない場合は、0 xffffffff を使用します。 |
| 32 |   | DataBuffer | DATABUFFER | データ バッファーを含む*ProviderId*します。 |

##### <a name="mbim_gsm_nmr"></a>MBIM_GSM_NMR

MBIM_GSM_NMR 構造体には、GSM の隣接するセルのネットワーク測定レポート (NMR) が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | この要素の後 NMR エントリの数。 |
| 4 |   | DataBuffer | DATABUFFER | NMR の配列がレコードとして指定された各、 [MBIM_GSM_NMR_INFO](#mbim_gsm_nmr_info)構造体。 |

##### <a name="mbim_gsm_nmr_info"></a>MBIM_GSM_NMR_INFO

MBIM_GSM_NMR_INFO 構造体には、隣接する GSM セルについての情報が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 呼ばれる数値 (0 ~ 9) の文字列に、この構造体の先頭からのオフセット (バイト単位) が計算される*ProviderId*プロバイダーのネットワーク id を表します。 この文字列は、3 桁 Mobile 国コード (MCC) と、2 つの連結または 3 桁モバイル ネットワーク コード mnc (も)。 このメンバーがない場合は NULL を指定できます*ProviderId*情報が返されます。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 使用サイズ*ProviderId*します。 |
| 8 | 4 | LocationAreaCode | UINT32 | 場所の市外局番 (0 ~ 65535)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 12 | 4 | CellID | UINT32 | セルの ID (0 ~ 65535) です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 16 | 4 | ARFCN | UINT32 | サービスのセル (0 ~ 1023) の絶対数の無線周波数チャネル。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 20 | 4 | BaseStationId | UINT32 | 提供のセル (0 ~ 63) のラジオ ベース ステーション ID です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 24 | 4 | RxLevel | UINT32 | セル (0 ~ 63) の場所、サービスの受信信号強度 <p>`X = 0, if RSS < -110 dBm`</p><p>`X = 63, if RSS > -47 dBm`</p><p>`X = integer [RSS + 110], if -110 <= RSS <= -47`</p> この情報が利用できない場合は、0 xffffffff を使用します。 |
| 28 |   | DataBuffer | DATABUFFER | データ バッファーを含む*ProviderId*します。 |

#### <a name="umts-cell-data-structures"></a>UMTS セルのデータ構造体

##### <a name="mbim_umts_serving_cell_info"></a>MBIM_UMTS_SERVING_CELL_INFO

MBIM_UMTS_SERVING_CELL_INFO 構造体には、UMTS サービング セルに関する情報が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 呼ばれる数値 (0 ~ 9) の文字列に、この構造体の先頭からのオフセット (バイト単位) が計算される*ProviderId*プロバイダーのネットワーク id を表します。 この文字列は、3 桁 Mobile 国コード (MCC) と、2 つの連結または 3 桁モバイル ネットワーク コード mnc (も)。 このメンバーがない場合は NULL を指定できます*ProviderId*情報が返されます。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 使用サイズ*ProviderId*します。 |
| 8 | 4 | LocationAreaCode | UINT32 | 場所の市外局番 (0 ~ 65535)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 12 | 4 | CellID | UINT32 | セルの ID (0-268435455)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 16 | 4 | FrequencyInfoUL | UINT32 | 周波数情報アップリンク (0-16383)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 20 | 4 | FrequencyInfoDL | UINT32 | 周波数情報ダウンリンク (0-16383)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 24 | 4 | FrequencyInfoNT | UINT32 | TDD (0-16383) の周波数情報です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 28 | 4 | UARFCN | UINT32 | UTRA 絶対無線周波数のチャネル番号サービング セル (0-16383)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 32 | 4 | PrimaryScramblingCode | UINT32 | プライマリ スクランブルのコード提供セル (0 ~ 511)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 36 | 4 | RSCP | INT32 | 受信したシグナル コードの機能を提供セル。 範囲は、1dBm の単位での-25 に-120 です。 この情報が利用できない場合は、0 を使用します。 |
| 40 | 4 | ECNO | INT32 | サービスがセルのノイズ比率にシグナル受信したエネルギー PN チップに受信した合計 CPICH のごとの比率です。 範囲は、-50 1dBm の単位、0 です。 この情報が利用できない場合は、1 を使用します。 |
| 44 | 4 | PathLoss | UINT32 | サービスのセル (46 173) のパスの損失。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 48 |   | DataBuffer | DATABUFFER | データ バッファーを含む*ProviderId*します。 |

##### <a name="mbim_umts_mrl"></a>MBIM_UMTS_MRL

MBIM_UMTS_MRL 構造体には、UMTS の隣接するセルの測定結果一覧 (MRL) が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | この要素の次 MRL エントリの数。 |
| 4 |   | DataBuffer | DATABUFFER | MRL の配列がレコードとして指定された各、 [MBIM_UMTS_MRL_INFO](#mbim_gsm_nmr_info)構造体。 |

##### <a name="mbim_umts_mrl_info"></a>MBIM_UMTS_MRL_INFO

MBIM_UMTS_MRL_INFO 構造体には、隣接する UMTS セルについての情報が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 呼ばれる数値 (0 ~ 9) の文字列に、この構造体の先頭からのオフセット (バイト単位) が計算される*ProviderId*プロバイダーのネットワーク id を表します。 この文字列は、3 桁 Mobile 国コード (MCC) と、2 つの連結または 3 桁モバイル ネットワーク コード mnc (も)。 このメンバーがない場合は NULL を指定できます*ProviderId*情報が返されます。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 使用サイズ*ProviderId*します。 |
| 8 | 4 | LocationAreaCode | UINT32 | 場所の市外局番 (0 ~ 65535)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 12 | 4 | CellID | UINT32 | セルの ID (0-268435455)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 16 | 4 | UARFCN | UINT32 | UTRA 絶対無線周波数のチャネル番号サービング セル (0-16383)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 20 | 4 | PrimaryScramblingCode | UINT32 | プライマリ スクランブルのコード提供セル (0 ~ 511)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 24 | 4 | RSCP | INT32 | 受信したシグナル コードの機能を提供セル。 範囲は、1dBm の単位での-25 に-120 です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 28 | 4 | ECNO | INT32 | サービスがセルのノイズ比率にシグナル受信したエネルギー PN チップに受信した合計 CPICH のごとの比率です。 範囲は、-50 1dBm の単位、0 です。 この情報が利用できない場合は、1 を使用します。 |
| 32 | 4 | PathLoss | UINT32 | サービスのセル (46 173) のパスの損失。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 36 |   | DataBuffer | DATABUFFER | データ バッファーを含む*ProviderId*します。 |

#### <a name="tdscdma-cell-data-structures"></a>TDSCDMA セルのデータ構造体

##### <a name="mbim_tdscdma_serving_cell_info"></a>MBIM_TDSCDMA_SERVING_CELL_INFO

MBIM_TDSCDMA_SERVING_CELL_INFO 構造体には、TDSCDMA サービング セルに関する情報が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 呼ばれる数値 (0 ~ 9) の文字列に、この構造体の先頭からのオフセット (バイト単位) が計算される*ProviderId*プロバイダーのネットワーク id を表します。 この文字列は、3 桁 Mobile 国コード (MCC) と、2 つの連結または 3 桁モバイル ネットワーク コード mnc (も)。 このメンバーがない場合は NULL を指定できます*ProviderId*情報が返されます。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 使用サイズ*ProviderId*します。 |
| 8 | 4 | LocationAreaCode | UINT32 | 場所の市外局番 (0 ~ 65535)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 12 | 4 | CellID | UINT32 | セルの ID (0-268435455)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 16 | 4 | UARFCN | UINT32 | UTRA 絶対無線周波数のチャネル番号サービング セル (0-16383)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 20 | 4 | CellParameterID | UINT32 | セルのパラメーター ID (0 ~ 127)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 24 | 4 | TimingAdvance | UINT32 | タイミングの詳細 (0 ~ 1023)。 このメンバーは、すべてのタイム スロットの値が同じです。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 28 | 4 | RSCP | INT32 | 受信したシグナル コードの機能を提供セル。 範囲でフィルター処理する Q8 L3 1dBm の単位での-25 に-120 です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 32 | 4 | PathLoss | UINT32 | サービスのセル (46 ~ 158) のパスの損失。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 36 |   | DataBuffer | DATABUFFER | データ バッファーを含む*ProviderId*します。 |

##### <a name="mbim_tdscdma_mrl"></a>MBIM_TDSCDMA_MRL

MBIM_TDSCDMA_MRL 構造体には、隣接する TDSCDMA セルの測定結果一覧 (MRL) が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | この要素の次 MRL エントリの数。 |
| 4 |   | DataBuffer | DATABUFFER | MRL の配列がレコードとして指定された各、 [MBIM_TDSCDMA_MRL_INFO](#mbim_tdscdma_mrl_info)構造体。 |

##### <a name="mbim_tdscdma_mrl_info"></a>MBIM_TDSCDMA_MRL_INFO

MBIM_TDSCDMA_MRL_INFO 構造体には、隣接する TDSCDMA セルについての情報が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 呼ばれる数値 (0 ~ 9) の文字列に、この構造体の先頭からのオフセット (バイト単位) が計算される*ProviderId*プロバイダーのネットワーク id を表します。 この文字列は、3 桁 Mobile 国コード (MCC) と、2 つの連結または 3 桁モバイル ネットワーク コード mnc (も)。 このメンバーがない場合は NULL を指定できます*ProviderId*情報が返されます。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 使用サイズ*ProviderId*します。 |
| 8 | 4 | LocationAreaCode | UINT32 | 場所の市外局番 (0 ~ 65535)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 12 | 4 | CellID | UINT32 | セルの ID (0-268435455)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 16 | 4 | UARFCN | UINT32 | UTRA 絶対無線周波数のチャネル番号サービング セル (0-16383)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 20 | 4 | CellParameterID | UINT32 | セルのパラメーター ID (0 ~ 127)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 24 | 4 | TimingAdvance | UINT32 | タイミングの詳細 (0 ~ 1023)。 このメンバーは、すべてのタイム スロットの値が同じです。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 28 | 4 | RSCP | INT32 | 受信したシグナル コードの機能を提供セル。 範囲でフィルター処理する Q8 L3 1dBm の単位での-25 に-120 です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 32 | 4 | PathLoss | UINT32 | サービスのセル (46 ~ 158) のパスの損失。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 36 |   | DataBuffer | DATABUFFER | データ バッファーを含む*ProviderId*します。 |

#### <a name="lte-cell-data-structures"></a>LTE セルのデータ構造体

##### <a name="mbim_lte_serving_cell_info"></a>MBIM_LTE_SERVING_CELL_INFO

MBIM_LTE_SERVING_CELL_INFO 構造体には、LTE サービング セルに関する情報が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 呼ばれる数値 (0 ~ 9) の文字列に、この構造体の先頭からのオフセット (バイト単位) が計算される*ProviderId*プロバイダーのネットワーク id を表します。 この文字列は、3 桁 Mobile 国コード (MCC) と、2 つの連結または 3 桁モバイル ネットワーク コード mnc (も)。 このメンバーがない場合は NULL を指定できます*ProviderId*情報が返されます。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 使用サイズ*ProviderId*します。 |
| 8 | 4 | CellID | UINT32 | セルの ID (0-268435455)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 12 | 4 | EARFCN | UINT32 | サービスのセル (0 ~ 65535) の無線周波数チャネルの数。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 16 | 4 | PhysicalCellID | UINT32 | 物理セル ID (0-503)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 20 | 4 | TAC | UINT32 | 追跡の市外局番 (0 ~ 65535)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 24 | 4 | RSRP | INT32 | 平均の参照信号は、電源を受信しました。 範囲は、1dBm の単位での-44 に-140 です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 28 | 4 | RSRQ | INT32 | 平均の参照信号は、品質を受信しました。 範囲は、1dBm の単位で-3-20 です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 32 | 4 | TimingAdvance | UINT32 | タイミングの詳細 (0 ~ 255)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 36 |   | DataBuffer | DATABUFFER | データ バッファーを含む*ProviderId*します。 |

##### <a name="mbim_lte_mrl"></a>MBIM_LTE_MRL

MBIM_LTE_MRL 構造体には、隣接する LTE セルの測定結果一覧 (MRL) が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | この要素の次 MRL エントリの数。 |
| 4 |   | DataBuffer | DATABUFFER | MRL の配列がレコードとして指定された各、 [MBIM_LTE_MRL_INFO](#mbim_lte_mrl_info)構造体。 |

##### <a name="mbim_lte_mrl_info"></a>MBIM_LTE_MRL_INFO

MBIM_LTE_MRL_INFO 構造体には、隣接する LTE セルについての情報が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ProviderIdOffset | OFFSET | 呼ばれる数値 (0 ~ 9) の文字列に、この構造体の先頭からのオフセット (バイト単位) が計算される*ProviderId*プロバイダーのネットワーク id を表します。 この文字列は、3 桁 Mobile 国コード (MCC) と、2 つの連結または 3 桁モバイル ネットワーク コード mnc (も)。 このメンバーがない場合は NULL を指定できます*ProviderId*情報が返されます。 |
| 4 | 4 | ProviderIdSize | SIZE(0-12) | 使用サイズ*ProviderId*します。 |
| 8 | 4 | CellID | UINT32 | セルの ID (0-268435455)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 12 | 4 | EARFCN | UINT32 | サービスのセル (0 ~ 65535) の無線周波数チャネルの数。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 16 | 4 | PhysicalCellID | UINT32 | 物理セル ID (0-503)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 20 | 4 | TAC | UINT32 | 追跡の市外局番 (0 ~ 65535)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 24 | 4 | RSRP | INT32 | 平均の参照信号は、電源を受信しました。 範囲は、1dBm の単位での-44 に-140 です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 28 | 4 | RSRQ | INT32 | 平均の参照信号は、品質を受信しました。 範囲は、1dBm の単位で-3-20 です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 32 |   | DataBuffer | DATABUFFER | データ バッファーを含む*ProviderId*します。 |

#### <a name="cdma-cell-data-structures"></a>CDMA セルのデータ構造体

##### <a name="mbim_cdma_mrl"></a>MBIM_CDMA_MRL

MBIM_CDMA_MRL 構造体には、提供していると、隣接するセルの CDMA の測定結果一覧 (MRL) が含まれています。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ElementCount (EC) | UINT32 | この要素の次 MRL エントリの数。 |
| 4 |   | DataBuffer | DATABUFFER | MRL の配列がレコードとして指定された各、 [MBIM_CDMA_MRL_INFO](#mbim_cdma_mrl_info)構造体。 |

##### <a name="mbim_cdma_mrl_info"></a>MBIM_CDMA_MRL_INFO

MBIM_CDMA_MRL_INFO データ構造体は、CDMA2000 ネットワークの種類に適しています。 同時に 1 つ以上の CDMA2000 サービング セルがあります。 同じリスト内のセルを提供していると隣接するセルの両方が返されます。 **ServingCellFlag**フィールドは、セルがサービング セルかどうかを示します。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ServingCellFlag | UINT32 | これはサービス セルであるかどうかを示します。 1 の値を隣接するセル値が 0 の中にサービス セルの場合を示します。 (特に通話中に)、一度に 1 つ以上のサービスのセルが可能性があります。 |
| 4 | 4 | NID | UINT32 | ネットワーク ID (0 ~ 65535) です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 8 | 4 | SID | UINT32 | システム ID (0-32767)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 12 | 4 | BaseStationId | UINT32 | ベース ステーション ID (0 ~ 65535) です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 16 | 4 | BaseLatitude | UINT32 | 基地局緯度 (0-4194303) です。 これは、2 の補数表現、22 の下位ビット dword 値内で表される、0.25 秒単位でエンコードされます。 符号付きの値として北緯度は正です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 20 | 4 | BaseLongitude | UINT32 | 基地局経度 (8388607 0) です。 これは、2 の補数表現 dword 値の下位の 23 ビット内で表される、0.25 秒単位でエンコードされます。 符号付きの値としては、東部経度は正です。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 24 | 4 | RefPN | UINT32 | 基地局 PN 数 (0 ~ 511)。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 28 | 4 | GPSSeconds | UINT32 | GPS (秒)、または時刻を基地局からこの到着しました。 この情報が利用できない場合は、0 xffffffff を使用します。 |
| 32 | 4 | PilotStrength | UINT32 | パイロット (0 ~ 63) の信号強度。 この情報が利用できない場合は、0 xffffffff を使用します。 |

### <a name="unsolicited-event"></a>要請されていないイベント

適用できません。

### <a name="status-codes"></a>状態コード

この CID は汎用のステータス コードを使用して (の 9.4. 5. のセクションでは状態コードの使用を参照してください。[パブリック USB MBIM 標準](https://go.microsoft.com/fwlink/p/?linkid=842064))。

## <a name="mbim_cid_location_info_status"></a>MBIM_CID_LOCATION_INFO_STATUS

この CID をデバイスの場所を示す移動体通信情報の状態を取得します。 場所情報が変更された際に、請求の通知を配信するも使用可能性があります。

サービス:**MBB_UUID_BASIC_CONNECT_EXTENSIONS**

サービス UUID:**3d01dcc5-fef5-4d05-0d3a-bef7058e9aaf**

| CID | コマンド コード | 最小 OS バージョン |
| --- | --- | --- |
| MBIM_CID_LOCATION_INFO_STATUS | 12 | Windows 10 バージョン 1709 |

> [!NOTE]
> MBIM_CID_LOCATION_INFO_STATUS が定義されている Windows 10 バージョン 1709 以降しますが、OS によって現在サポートされていません。 モデムが、通知としてこのコマンドを送信できますが、OS は現在処理しないこと。

### <a name="parameters"></a>パラメーター

| | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | 適用なし | 該当なし |
| 応答 | Appliable されません。 | MBIM_LOCATION_INFO | MBIM_LOCATION_INFO |

### <a name="query"></a>クエリ

MBIM_COMMAND_MSG InformationBuffer は使用されません。 含まれています、MBIM_COMMAND_DONE の InformationBuffer、 [MBIM_LOCATION_INFO](#mbim_location_info)構造体。

### <a name="set"></a>Set

適用できません。

### <a name="response"></a>応答

#### <a name="mbim_location_info"></a>MBIM_LOCATION_INFO

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | LocationAreaCode | UINT32 | 現在の場所の GSM/UMTS 領域のコードです。 現在のシステム型が適用されない場合は、0 xffffffff を返します。 |
| 4 | 4 | TrackingAreaCode | UINT32 | 現在の場所の市外局番を追跡 LTE します。 現在のシステム型が適用されない場合は、0 xffffffff を返します。 |
| 8 | 4 | CellID | UINT32 | 携帯電話の塔の ID。 0 xffffffff を返すときに*CellID*は使用できません。 |

### <a name="unsolicited-events"></a>要請されていないイベント

InformationBuffer イベントには、MBIM_LOCATION_INFO 構造体が含まれています。

場合、このイベントが送信されるの値*場所市外局番*/*市外局番の追跡*有効な値に変更します。 このイベントを送信しない場合に*CellID*変更または*場所市外局番*/*市外局番の追跡*は無効になります。

### <a name="status-codes"></a>状態コード

この CID は汎用のステータス コードを使用して (の 9.4. 5. のセクションでは状態コードの使用を参照してください。[パブリック USB MBIM 標準](https://go.microsoft.com/fwlink/p/?linkid=842064))。

## <a name="oid_wwan_base_stations_info"></a>OID_WWAN_BASE_STATIONS_INFO

MBIM_CID_BASE_STATIONS_INFO の NDIS 相当するものは[OID_WWAN_BASE_STATIONS_INFO](oid-wwan-base-stations-info.md)します。

