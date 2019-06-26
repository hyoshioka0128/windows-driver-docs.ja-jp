---
title: MagneticStripeReaderErrorOccured
description: MagneticStripeReaderErrorOccured イベントでは、スキャンのエラーなどの磁気ストライプ リーダー (MSR) エラーがあるときに発生します。
ms.assetid: c2402411-1bbf-44c1-bf7f-813f6d967822
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: a8bafd029ac4bdbabc63cecc5dbe56559e3afddf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363373"
---
# <a name="magneticstripereadererroroccured"></a>MagneticStripeReaderErrorOccured

このイベントは、スキャンのエラーなどの磁気ストライプ リーダー (MSR) エラーがある場合に発生します。

## <a name="syntax"></a>構文

```cpp
typedef struct _MSR_ERROR_EVENT
{
    PosEventDataHeader Header;
    MsrTrackErrorType Track1Status;
    MsrTrackErrorType Track2Status;
    MsrTrackErrorType Track3Status;
    MsrTrackErrorType Track4Status;
    UnifiedPosErrorSeverity Severity;
    UnifiedPosErrorReason Reason;
    UINT32 ExtendedReason;
    MSR_DATA_RECEIVED CardData;
    wchar_t Message[MSR_ERROR_MAX_MESSAGE_LENGTH];
} MSR_ERROR_EVENT, *PMSR_ERROR_EVENT;
```

次の表では、このイベントのデータ バッファーのメモリ レイアウトを示します。

| メモリの値                                                                   | 説明                                                                                                                               |
|--------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000009                                                          | **EventType = PosEventType:。MagneticStripeReaderErrorOccurred**                                                               |
| UINT32                                                              | **DataLength** = sizeof(**PosEventDataHeader**) + sizeof(**MSR\_ERROR\_EVENT**)                                                |
| 32 ビット[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track1Status**                                                                                                               |
| 32 ビット[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track2Status**                                                                                                               |
| 32 ビット[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track3Status**                                                                                                               |
| 32 ビット[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track4Status**                                                                                                               |
| 32 ビット[UnifiedPosErrorSeverity](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicecommontypes/ne-pointofservicecommontypes-driverunifiedposerrorseverity)       | **重要度**                                                                                                                   |
| 32 ビット[UnifiedPosErrorReason](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicecommontypes/ne-pointofservicecommontypes-driverunifiedposerrorreason)           | **Reason**                                                                                                                     |
| UINT32                                                              | **拡張の理由**                                                                                                            |
| 32 ビット[MsrCardType](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrcardtype)                               | **CardType**                                                                                                                   |
| unsigned char                                                       | **Track1EncryptedDataLength**                                                                                                  |
| unsigned char                                                       | **Track2EncryptedDataLength**                                                                                                  |
| unsigned char                                                       | **Track3EncryptedDataLength**                                                                                                  |
| unsigned char                                                       | **Track4EncryptedDataLength**                                                                                                  |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track1EncryptedDataLength**トラック 1 の暗号化されたデータのバイト数                                                                  |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track2EncryptedDataLength**トラック 2 の暗号化されたデータのバイト数                                                                  |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track3EncryptedDataLength** 3 の暗号化された追跡データのバイト数                                                                  |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track4EncryptedDataLength** 4 の暗号化された追跡データのバイト数                                                                  |
| unsigned char                                                       | **Track1MaskedDataLength**                                                                                                     |
| unsigned char                                                       | **Track2MaskedDataLength**                                                                                                     |
| unsigned char                                                       | **Track3MaskedDataLength**                                                                                                     |
| unsigned char                                                       | **Track4MaskedDataLength**                                                                                                     |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track1MaskedDataLength**マスクのバイトが 1 つのデータを追跡                                                                        |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track2MaskedDataLength**マスクのバイト数が 2 つのデータを追跡                                                                        |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track3MaskedDataLength**バイトのマスクされた 3 つのデータを追跡します。                                                                        |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track4MaskedDataLength**マスクのバイト数が 4 つのデータを追跡                                                                        |
| unsigned char                                                       | **Track1DiscretionaryDataLength**                                                                                              |
| unsigned char                                                       | **Track2DiscretionaryDataLength**                                                                                              |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track1DiscretionaryDataLength**随意のバイトが 1 つのデータを追跡                                                          |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track2DiscretionaryDataLength**随意のバイト数が 2 つのデータを追跡                                                          |
| unsigned char                                                       | **CardAuthenicationDataLength** -埋め込みを含む、暗号化後にデータの長さ                                       |
| unsigned char                                                       | **CardAuthenticationDataAbsoluteLength** -(暗号化解除中にパディングを削除する必要する可能性があります) を暗号化する前にデータの長さ |
| unsigned char\[MSR\_追加\_セキュリティ\_情報\_データ\_サイズ\] | **CardAuthenticationDataAbsoluteLength**カードの認証データのバイト数                                                     |
| unsigned char                                                       | **AdditionalSecurityInformationLength**                                                                                        |
| unsigned char\[MSR\_追加\_セキュリティ\_情報\_サイズ\]       | **AdditionalSecurityInformationLength**バイトの追加のセキュリティ情報                                               |
| wchar\_T \[MSR\_エラー\_最大\_メッセージ\_長さ\]                       | 最大**MSR\_エラー\_最大\_メッセージ\_長さ**wchar\_エラーの t **Null**-メッセージのテキストの終了                                  |


## <a name="remarks"></a>注釈

スキャン エラーが発生するいくつかのスキャン データが取得された場合は、イベント データには、部分的なスキャン データが含まれています。

## <a name="requirements"></a>要件

**ヘッダー:** pointofservicedriverinterface.h
