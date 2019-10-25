---
title: MagneticStripeReaderErrorOccured
description: MagneticStripeReaderErrorOccured イベントは、スキャンエラーなどの磁気ストライプリーダー (MSR) エラーがある場合に発生します。
ms.assetid: c2402411-1bbf-44c1-bf7f-813f6d967822
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2db6d8d03132912d7804c31af70d7ffc90c24a8c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843127"
---
# <a name="magneticstripereadererroroccured"></a>MagneticStripeReaderErrorOccured

このイベントは、スキャンエラーなどの磁気ストライプリーダー (MSR) エラーがある場合に発生します。

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

次の表は、このイベントのデータバッファーのメモリレイアウトを示しています。

| メモリ値                                                                   | 説明                                                                                                                               |
|--------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000009                                                          | **EventType = PosEventType:: MagneticStripeReaderErrorOccurred**                                                               |
| UINT32                                                              | **DataLength** = Sizeof (**PosEventDataHeader**) + SIZEOF (**MSR\_ERROR\_イベント**)                                                |
| 32ビット[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track1Status**                                                                                                               |
| 32ビット[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track2Status**                                                                                                               |
| 32ビット[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track3Status**                                                                                                               |
| 32ビット[MsrTrackErrorType](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrtrackerrortype)                   | **Track4Status**                                                                                                               |
| 32ビット[UnifiedPosErrorSeverity](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicecommontypes/ne-pointofservicecommontypes-driverunifiedposerrorseverity)       | **順**                                                                                                                   |
| 32ビット[UnifiedPosErrorReason](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicecommontypes/ne-pointofservicecommontypes-driverunifiedposerrorreason)           | **理由**                                                                                                                     |
| UINT32                                                              | **拡張理由**                                                                                                            |
| 32-bit [Msrcardtype](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrcardtype)                               | **CardType**                                                                                                                   |
| unsigned char                                                       | **Track1EncryptedDataLength**                                                                                                  |
| unsigned char                                                       | **Track2EncryptedDataLength**                                                                                                  |
| unsigned char                                                       | **Track3EncryptedDataLength**                                                                                                  |
| unsigned char                                                       | **Track4EncryptedDataLength**                                                                                                  |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | 暗号化されたトラック1データの**Track1EncryptedDataLength**バイト数                                                                  |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | 暗号化されたトラック2データの**Track2EncryptedDataLength**バイト数                                                                  |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | 暗号化されたトラック3データの**Track3EncryptedDataLength**バイト数                                                                  |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | 暗号化されたトラック4データの**Track4EncryptedDataLength**バイト数                                                                  |
| unsigned char                                                       | **Track1MaskedDataLength**                                                                                                     |
| unsigned char                                                       | **Track2MaskedDataLength**                                                                                                     |
| unsigned char                                                       | **Track3MaskedDataLength**                                                                                                     |
| unsigned char                                                       | **Track4MaskedDataLength**                                                                                                     |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | マスクされるトラック1データの**Track1MaskedDataLength**バイト数                                                                        |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | マスクされるトラック2データの**Track2MaskedDataLength**バイト数                                                                        |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | マスクされるトラック3データの**Track3MaskedDataLength**バイト数                                                                        |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | マスクされるトラック4データの**Track4MaskedDataLength**バイト数                                                                        |
| unsigned char                                                       | **Track1DiscretionaryDataLength**                                                                                              |
| unsigned char                                                       | **Track2DiscretionaryDataLength**                                                                                              |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | 随意トラック1データの**Track1DiscretionaryDataLength**バイト数                                                          |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | 随意トラック2データの**Track2DiscretionaryDataLength**バイト数                                                          |
| unsigned char                                                       | **Cardauthenicationdatalength** -暗号化後のデータの長さ (埋め込みを含む)                                       |
| unsigned char                                                       | **CardAuthenticationDataAbsoluteLength** -暗号化前のデータの長さ (暗号化解除中にパディングを取り除くために必要になる場合があります) |
| 署名されていない char\[MSR\_追加\_セキュリティ\_情報\_データ\_サイズ\] | **CardAuthenticationDataAbsoluteLength** bytes authentication data (カード認証データのバイト数)                                                     |
| unsigned char                                                       | **AdditionalSecurityInformationLength**                                                                                        |
| 署名されていない char\[MSR\_追加\_セキュリティ\_情報\_サイズ\]       | 追加のセキュリティ情報の**Additionalsecurityinformationlength**バイト                                               |
| wchar\_T \[MSR\_エラー\_最大\_メッセージ\_長さ\]                       | 最大**MSR\_エラー\_最大\_メッセージ\_長さ**wchar\_エラーの**Null**で終わるメッセージテキスト                                  |


## <a name="remarks"></a>注釈

スキャンエラーが発生し、一部のスキャンデータが取得された場合、イベントデータには部分スキャンデータが含まれます。

## <a name="requirements"></a>要件

**ヘッダー:** pointofservicedriverinterface
