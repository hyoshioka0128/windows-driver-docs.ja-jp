---
title: 送信操作
description: 送信操作
ms.assetid: 84af0abc-c8f2-47d4-b368-7b0216600c95
keywords:
- 送信操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b2840ade07e8e9f7531afdc4fe3bf329c1aadae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365762"
---
# <a name="send-operations"></a>送信操作




 

呼び出すことによって開始された後の関連付け操作を実行するときに[ *Dot11ExtIhvPerformPostAssociate*](https://msdn.microsoft.com/library/windows/hardware/ff547492)、IHV 拡張機能の DLL は、ワイヤレス LAN (WLAN) アダプターを介してパケットを送信できます。 詳細については、後の関連付け操作は、次を参照してください。[後関連付け操作](post-association-operations.md)します。

通常、DLL のセキュリティにパケットを送信データ ポートの認証のためのアクセス ポイント (AP) を介して有効になっているアルゴリズムを使用して[ **Dot11ExtSetAuthAlgorithm**](https://msdn.microsoft.com/library/windows/hardware/ff547571)します。 拡張 DLL の IHV 呼び出し**Dot11ExtSetAuthAlgorithm**関連付け前の操作中にします。 この操作の詳細については、次を参照してください。[関連付け前操作](pre-association-operations.md)します。

**注**  Windows Vista の IHV 拡張機能の DLL は、基本的なサービスのインフラストラクチャ (BSS) ネットワークの設定のみをサポートします。

 

パケットを送信するときに、IHV 拡張 DLL は次のガイドラインに従う必要があります。

-   IHV 拡張機能の DLL は、802.11 メディア アクセス制御 (MAC) のヘッダー、LLC (必要に応じて) カプセル化、およびペイロード データを含む、完全な 802.11 データ パケットのメモリを割り当てる必要があります。

    次の表では、フィールドと 802.11 MAC ヘッダー内のサブフィールドを IHV 拡張機能の DLL または WLAN アダプターによって設定について説明します。

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
    <th align="left">サブフィールドの名前</th>
    <th align="left">拡張 DLL の IHV によって設定します。</th>
    <th align="left">WLAN アダプターによって設定します。</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>Frame コントロール</p></td>
    <td align="left"><p>プロトコルのバージョン</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>Frame コントロール</p></td>
    <td align="left"><p>型</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Frame コントロール</p></td>
    <td align="left"><p>サブタイプ</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>Frame コントロール</p></td>
    <td align="left"><p>DS に</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Frame コントロール</p></td>
    <td align="left"><p>DS から</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>Frame コントロール</p></td>
    <td align="left"><p>複数のフラグメント</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Frame コントロール</p></td>
    <td align="left"><p>再試行</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>Frame コントロール</p></td>
    <td align="left"><p>電源管理</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Frame コントロール</p></td>
    <td align="left"><p>多くのデータ</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>Frame コントロール</p></td>
    <td align="left"><p>保護されたフレーム</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>Frame コントロール</p></td>
    <td align="left"><p>[オーダー]</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>実行時間と ID</p></td>
    <td align="left"></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>住所 1</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>住所 2</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>住所 3</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>シーケンス コントロール</p></td>
    <td align="left"><p>フラグメントの数</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>シーケンス コントロール</p></td>
    <td align="left"><p>Sequence Number</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    </tbody>
    </table>

     

-   IHV 拡張 DLL の呼び出し、 [ **Dot11ExtSendPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff547563)ワイヤレス LAN (WLAN) アダプターを介してパケットを送信する関数。 DLL は、関数のパケットを識別する一意のハンドル値を渡します*hSendCompletion*パラメーター。 通常、DLL がパケットを含む、割り当てられたバッファーのアドレスを渡します、 *hSendCompletion*パラメーター。
    **注**  呼び出しを通じて、ユニキャスト パケットのみを送信できる、 [ **Dot11ExtSendPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff547563)関数。

     

-   オペレーティング システムを呼び出す WLAN アダプターには、パケットが送信、ときに、 [ *Dot11ExtIhvSendPacketCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff547516)関数。 オペレーティング システムは、パケットのハンドル値を渡します、 *hSendCompletion*関数のパラメーター。 このハンドルの値は呼び出しで IHV 拡張 DLL で使用される同じ値になります[ **Dot11ExtSendPacket**](https://msdn.microsoft.com/library/windows/hardware/ff547563)します。

    ときに[ *Dot11ExtIhvSendPacketCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff547516)が呼び出されると、IHV 拡張機能の DLL は、パケットを割り当てられたメモリを解放する必要があります。

    **注**  IHV 拡張 DLL を経由して送信パケットに割り当てられたリソースを解放する必要があります[ **Dot11ExtSendPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff547563)に対応する呼び出しまで[*Dot11ExtIhvSendPacketCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff547516)されます。

     

 

 





