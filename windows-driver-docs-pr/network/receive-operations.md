---
title: 受信操作
description: 受信操作
ms.assetid: 9ec2ba38-36dd-42d2-b0a8-0abe4d1bb847
keywords:
- 受信操作 WDK ネイティブ 802.11 IHV 拡張 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed6f88553eea6c202702b93b1f441e0bd5f9f77c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843471"
---
# <a name="receive-operations"></a>受信操作




 

[*Dot11ExtIhvPerformPostAssociate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)の呼び出しによって開始される関連付け後の操作を実行すると、オペレーティングシステムは[*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet)関数を呼び出して、を通じて受信した hv 拡張 DLL にパケットを転送します。ワイヤレス LAN (WLAN) アダプター。 関連付け後の操作の詳細については、「[関連付け後の操作](post-association-operations.md)」を参照してください。

パケットを受信するために、IHV 拡張 DLL は[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)を呼び出して、1つ以上の IEEE EtherTypes の一覧を登録する必要があります。 この一覧のエントリと一致する EtherType を使用してパケットを受信すると、オペレーティングシステムは[*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet)関数を呼び出し、関数の*pvInBuffer*パラメーターを使用してパケットバッファーを渡します。

DLL が事前関連付け操作を完了する前に、IHV 拡張 DLL が[**Dot11ExtSetEtherTypeHandling**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling)を呼び出す必要がある  に**注意**してください。 この操作の詳細については、「[事前関連付け操作](pre-association-operations.md)」を参照してください。

 

[*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet)が呼び出されると、 *pvInBuffer*パラメーターは、802.11 パケット全体を含むオペレーティングシステムによって割り当てられたバッファーを指します。これには、メディアアクセスコントロール (MAC) ヘッダー、必要に応じて、が含まれます。およびペイロードデータ。

IHV 拡張 DLL は、 [*Dot11ExtIhvReceivePacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet)の呼び出し内から受信パケットに応答を送信できます。 この場合、DLL は「[送信操作](send-operations.md)」で説明されているガイドラインに従う必要があります。

 

 





