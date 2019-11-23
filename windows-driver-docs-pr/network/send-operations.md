---
title: 送信操作
description: 送信操作
ms.assetid: 84af0abc-c8f2-47d4-b368-7b0216600c95
keywords:
- 送信操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16311a14c0c3a12a2cfc30ad1e8d6c43fdd20c0e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841982"
---
# <a name="send-operations"></a>送信操作




 

[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)の呼び出しによって開始された関連付け後の操作を実行すると、IHV 拡張 DLL は、ワイヤレス LAN (WLAN) アダプターを介してパケットを送信できます。 関連付け後の操作の詳細については、「[関連付け後の操作](post-association-operations.md)」を参照してください。

通常、DLL は、 [**Dot11ExtSetAuthAlgorithm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm)によって有効になっているアルゴリズムを使用して、データポート認証のためにセキュリティパケットをアクセスポイント (AP) に送信します。 IHV 拡張 DLL は、関連付け前の操作中に**Dot11ExtSetAuthAlgorithm**を呼び出します。 この操作の詳細については、「[事前関連付け操作](pre-association-operations.md)」を参照してください。

**注**  Windows Vista では、IHV 拡張 DLL は、インフラストラクチャの基本サービスセット (BSS) ネットワークのみをサポートしています。

 

パケットを送信する場合、IHV 拡張 DLL は次のガイドラインに従う必要があります。

-   IHV 拡張 DLL は、802.11 データパケット全体のメモリを割り当てる必要があります。これには、802.11 メディアアクセスコントロール (MAC) ヘッダー、必要に応じての接続のカプセル化、およびペイロードデータが含まれます。

    次の表では、802.11 MAC ヘッダー内のフィールドとサブフィールドを、IHV 拡張 DLL または WLAN アダプターによって設定されています。

    <table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">フィールド名</th>
    <th align="left">サブフィールド名</th>
    <th align="left">IHV 拡張 DLL による設定</th>
    <th align="left">WLAN アダプターによる設定</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>フレームコントロール</p></td>
    <td align="left"><p>プロトコルのバージョン</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>フレームコントロール</p></td>
    <td align="left"><p>種類</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>フレームコントロール</p></td>
    <td align="left"><p>内部</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>フレームコントロール</p></td>
    <td align="left"><p>DS に</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>フレームコントロール</p></td>
    <td align="left"><p>DS から</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>フレームコントロール</p></td>
    <td align="left"><p>その他のフラグメント</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>フレームコントロール</p></td>
    <td align="left"><p>再試行</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>フレームコントロール</p></td>
    <td align="left"><p>Pwr の場合</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>フレームコントロール</p></td>
    <td align="left"><p>その他のデータ</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>フレームコントロール</p></td>
    <td align="left"><p>保護されたフレーム</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>フレームコントロール</p></td>
    <td align="left"><p>[オーダー]</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>期間/ID</p></td>
    <td align="left"></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>アドレス1</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>アドレス2</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>アドレス3</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>シーケンスコントロール</p></td>
    <td align="left"><p>フラグメント番号</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>シーケンスコントロール</p></td>
    <td align="left"><p>Sequence Number</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    </tbody>
    </table>

     

-   IHV 拡張 DLL は、 [**Dot11ExtSendPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet)関数を呼び出して、ワイヤレス LAN (WLAN) アダプター経由でパケットを送信します。 DLL は、パケットを識別する一意のハンドル値を関数の*Hsendcompletion*パラメーターに渡します。 通常、DLL は、パケットを含む割り当てられたバッファーのアドレスを*Hsendcompletion*パラメーターに渡します。
    [**Dot11ExtSendPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet)関数への呼び出しを通じて送信できるのは、ユニキャストパケットのみであることに**注意**してください  。

     

-   WLAN アダプターがパケットを送信すると、オペレーティングシステムは[*Dot11ExtIhvSendPacketCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion)関数を呼び出します。 オペレーティングシステムは、パケットのハンドル値を関数の*Hsendcompletion*パラメーターに渡します。 このハンドル値は、 [**Dot11ExtSendPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet)の呼び出しで IHV 拡張 DLL によって使用される値と同じになります。

    [*Dot11ExtIhvSendPacketCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion)が呼び出されると、IHV 拡張 DLL はパケットに割り当てられたメモリを解放する必要があります。

    [**Dot11ExtSendPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet)を介して送信されたパケットに割り当てられたリソースは、 [*Dot11ExtIhvSendPacketCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion)への対応する呼び出しが行われるまで解放されない  **ことに注意**してください。

     

 

 





