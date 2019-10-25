---
title: MagneticStripeReaderDataReceived
description: MagneticStripeReaderDataReceived イベントは、正常に実行された磁気ストライプリーダー (MSR) スキャンイベントの後に発生します。
ms.assetid: 5074669c-3914-4d15-983b-d979c7f88b21
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0c82de8f8149b208fb8d26cad7101e8617ca5770
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843574"
---
# <a name="magneticstripereaderdatareceived"></a>MagneticStripeReaderDataReceived

このイベントは、正常に実行された磁気ストライプリーダー (MSR) スキャンイベントの後に発生します。

## <a name="syntax"></a>構文

```cpp
typedef struct _MSR_DATA_RECEIVED {
    MsrCardType CardType;
    unsigned char Track1EncryptedDataLength;
    unsigned char Track2EncryptedDataLength;
    unsigned char Track3EncryptedDataLength;
    unsigned char Track4EncryptedDataLength;
    unsigned char Track1EncryptedData[MSR_TRACK_SIZE];
    unsigned char Track2EncryptedData[MSR_TRACK_SIZE];
    unsigned char Track3EncryptedData[MSR_TRACK_SIZE];
    unsigned char Track4EncryptedData[MSR_TRACK_SIZE];
    unsigned char Track1MaskedDataLength;
    unsigned char Track2MaskedDataLength;
    unsigned char Track3MaskedDataLength;
    unsigned char Track4MaskedDataLength;
    unsigned char Track1MaskedData[MSR_TRACK_SIZE];
    unsigned char Track2MaskedData[MSR_TRACK_SIZE];
    unsigned char Track3MaskedData[MSR_TRACK_SIZE];
    unsigned char Track4MaskedData[MSR_TRACK_SIZE];
    unsigned char Track1DiscretionaryDataLength;
    unsigned char Track2DiscretionaryDataLength;
    unsigned char Track1DiscretionaryData[MSR_TRACK_SIZE];
    unsigned char Track2DiscretionaryData[MSR_TRACK_SIZE];
    unsigned char CardAuthenicationDataLength; // Length of data after encryption, may include padding.
    unsigned char CardAuthenticationDataAbsoluteLength; // Length of data before encryption, may be needed to strip padding on decryption.
    unsigned char CardAuthenicationData[MSR_CARD_AUTHENTICATION_DATA_SIZE];
    unsigned char AdditionalSecurityInformationLength;
    unsigned char AdditionalSecurityInformation[MSR_ADDITIONAL_SECURITY_INFORMATION_SIZE];
} MSR_DATA_RECEIVED, *PMSR_DATA_RECEIVED;
```

次の表は、このイベントのデータバッファーのメモリレイアウトを示しています。

| メモリ値 | 説明 
|---|---|
| 0x00000008                                                          | **EventType = PosEventType:: MagneticStripeReaderDataReceived**                                                                       |
| UINT32                                                              | **DataLength** = Sizeof (**PosEventDataHeader**) + SIZEOF (**MSR\_データ\_受信**)                                                     |
| 32-bit MsrCardType                                                  | [MsrCardType](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrcardtype)                                                                                                        |
| unsigned char                                                       | **Track1EncryptedDataLength** - [msrdataencryption](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption)が**Msrdataencryption\_None**の場合、常にゼロ (0) になります。 |
| unsigned char                                                       | **Track2EncryptedDataLength** - [msrdataencryption](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption)が**Msrdataencryption\_None**の場合、常にゼロ (0) になります。 |
| unsigned char                                                       | **Track3EncryptedDataLength** - [msrdataencryption](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption)が**Msrdataencryption\_None**の場合、常にゼロ (0) になります。 |
| unsigned char                                                       | **Track4EncryptedDataLength** - [msrdataencryption](https://docs.microsoft.com/windows-hardware/drivers/ddi/pointofservicedriverinterface/ne-pointofservicedriverinterface-_msrdataencryption)が**Msrdataencryption\_None**の場合、常にゼロ (0) になります。 |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | 暗号化されたトラック1データの**Track1EncryptedDataLength**バイト数                                                                         |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | 暗号化されたトラック2データの**Track2EncryptedDataLength**バイト数                                                                         |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | 暗号化されたトラック3データの**Track3EncryptedDataLength**バイト数                                                                         |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | 暗号化されたトラック4データの**Track4EncryptedDataLength**バイト数                                                                         |
| unsigned char                                                       | **Track1MaskedDataLength**                                                                                                            |
| unsigned char                                                       | **Track2MaskedDataLength**                                                                                                            |
| unsigned char                                                       | **Track3MaskedDataLength**                                                                                                            |
| unsigned char                                                       | **Track4MaskedDataLength**                                                                                                            |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | マスクされるトラック1データの**Track1MaskedDataLength**バイト数                                                                               |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | マスクされるトラック2データの**Track2MaskedDataLength**バイト数                                                                               |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | マスクされるトラック3データの**Track3MaskedDataLength**バイト数                                                                               |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | マスクされるトラック4データの**Track4MaskedDataLength**バイト数                                                                               |
| unsigned char                                                       | **Track1DiscretionaryDataLength** – **MagneticStripeReaderIsDecodeDataEnabled**が false の場合、常にゼロ (0) になります。                |
| unsigned char                                                       | **Track2DiscretionaryDataLength**– **MagneticStripeReaderIsDecodeDataEnabled**が false の場合、常にゼロ (0) になります。                 |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | 随意トラック1データの**Track1DiscretionaryDataLength**バイト数                                                                 |
| 署名されていない char \[MSR\_追跡\_サイズ\]                                  | 随意トラック2データの**Track2DiscretionaryDataLength**バイト数                                                                 |
| unsigned char                                                       | **Cardauthenicationdatalength** -バイト単位の暗号化されたデータの長さ (埋め込みを含む)                                            |
| unsigned char                                                       | **CardAuthenticationDataAbsoluteLength** -暗号化されていないデータの長さ (バイト単位) (暗号化解除中にパディングを取り除く必要がある場合があります)  |
| 署名されていない char\[MSR\_追加\_セキュリティ\_情報\_データ\_サイズ\] | **CardAuthenticationDataAbsoluteLength** bytes authentication data (カード認証データのバイト数)                                                            |
| unsigned char                                                       | **AdditionalSecurityInformationLength**                                                                                               |
| 署名されていない char\[MSR\_追加\_セキュリティ\_情報\_サイズ\]       | 追加のセキュリティ情報の**Additionalsecurityinformationlength**バイト                                                      |

## <a name="requirements"></a>要件

**ヘッダー:** pointofservicedriverinterface
