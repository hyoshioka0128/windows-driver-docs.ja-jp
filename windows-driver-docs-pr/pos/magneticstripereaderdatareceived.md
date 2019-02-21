---
title: MagneticStripeReaderDataReceived
description: 成功の磁気ストライプ リーダー (MSR) がイベントをスキャンした後、MagneticStripeReaderDataReceived イベントが発生します。
ms.assetid: 5074669c-3914-4d15-983b-d979c7f88b21
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: eab2897ea3ef584edc4224118d951e8fa23fd915
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551991"
---
# <a name="magneticstripereaderdatareceived"></a>MagneticStripeReaderDataReceived

成功の磁気ストライプ リーダー (MSR) がイベントをスキャンした後、このイベントが発生します。

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

次の表では、このイベントのデータ バッファーのメモリ レイアウトを示します。

| メモリの値 | 説明 
|---|---|
| 0x00000008                                                          | **EventType = PosEventType:。MagneticStripeReaderDataReceived**                                                                       |
| UINT32                                                              | **DataLength** = sizeof(**PosEventDataHeader**) + sizeof(**MSR\_DATA\_RECEIVED**)                                                     |
| 32 ビット MsrCardType                                                  | [MsrCardType](https://msdn.microsoft.com/library/windows/hardware/dn772167)                                                                                                        |
| unsigned char                                                       | **Track1EncryptedDataLength**の場合、ゼロ (0) を必ずは[MsrDataEncryption](https://msdn.microsoft.com/library/windows/hardware/dn772169)は**MsrDataEncryption\_None**します。 |
| unsigned char                                                       | **Track2EncryptedDataLength**の場合、ゼロ (0) を必ずは[MsrDataEncryption](https://msdn.microsoft.com/library/windows/hardware/dn772169)は**MsrDataEncryption\_None**します。 |
| unsigned char                                                       | **Track3EncryptedDataLength**の場合、ゼロ (0) を必ずは[MsrDataEncryption](https://msdn.microsoft.com/library/windows/hardware/dn772169)は**MsrDataEncryption\_None**します。 |
| unsigned char                                                       | **Track4EncryptedDataLength**の場合、ゼロ (0) を必ずは[MsrDataEncryption](https://msdn.microsoft.com/library/windows/hardware/dn772169)は**MsrDataEncryption\_None**します。 |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track1EncryptedDataLength**トラック 1 の暗号化されたデータのバイト数                                                                         |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track2EncryptedDataLength**トラック 2 の暗号化されたデータのバイト数                                                                         |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track3EncryptedDataLength** 3 の暗号化された追跡データのバイト数                                                                         |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track4EncryptedDataLength** 4 の暗号化された追跡データのバイト数                                                                         |
| unsigned char                                                       | **Track1MaskedDataLength**                                                                                                            |
| unsigned char                                                       | **Track2MaskedDataLength**                                                                                                            |
| unsigned char                                                       | **Track3MaskedDataLength**                                                                                                            |
| unsigned char                                                       | **Track4MaskedDataLength**                                                                                                            |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track1MaskedDataLength**マスクのバイトが 1 つのデータを追跡                                                                               |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track2MaskedDataLength**マスクのバイト数が 2 つのデータを追跡                                                                               |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track3MaskedDataLength**バイトのマスクされた 3 つのデータを追跡します。                                                                               |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track4MaskedDataLength**マスクのバイト数が 4 つのデータを追跡                                                                               |
| unsigned char                                                       | **Track1DiscretionaryDataLength** – 場合、ゼロ (0) を必ずは**MagneticStripeReaderIsDecodeDataEnabled**は false です。                |
| unsigned char                                                       | **Track2DiscretionaryDataLength**– 場合、ゼロ (0) を必ずは**MagneticStripeReaderIsDecodeDataEnabled**は false です。                 |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track1DiscretionaryDataLength**随意のバイトが 1 つのデータを追跡                                                                 |
| unsigned char \[MSR\_トラック\_サイズ\]                                  | **Track2DiscretionaryDataLength**随意のバイト数が 2 つのデータを追跡                                                                 |
| unsigned char                                                       | **CardAuthenicationDataLength** -埋め込みを含むバイトの暗号化されたデータの長さ                                            |
| unsigned char                                                       | **CardAuthenticationDataAbsoluteLength** -バイト (暗号化解除中にパディングを削除する必要があります) で暗号化されていないデータの長さ  |
| unsigned char\[MSR\_追加\_セキュリティ\_情報\_データ\_サイズ\] | **CardAuthenticationDataAbsoluteLength**カードの認証データのバイト数                                                            |
| unsigned char                                                       | **AdditionalSecurityInformationLength**                                                                                               |
| unsigned char\[MSR\_追加\_セキュリティ\_情報\_サイズ\]       | **AdditionalSecurityInformationLength**バイトの追加のセキュリティ情報                                                      |

## <a name="requirements"></a>要件

**ヘッダー:** pointofservicedriverinterface.h
