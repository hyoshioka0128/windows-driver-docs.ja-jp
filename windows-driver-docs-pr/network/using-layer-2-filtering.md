---
title: レイヤー 2 フィルターの使用
description: レイヤー 2 フィルターの使用
ms.assetid: 679E6DE2-4EFB-44F6-936D-2BF611BC9726
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a0ddbda562aa2979e4b5e4ce109beb38fb3af17
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842989"
---
# <a name="using-layer-2-filtering"></a>レイヤー 2 フィルターの使用

レイヤー2のフィルター処理は、windows 8 以降のバージョンの Windows でサポートされています。

この WFP 機能では、レイヤー2の MAC ヘッダーのフィールドをフィルター処理できます。 これらのレイヤーは、ホストコンピューターによって送受信されるすべてのパケットに対して、パケット単位で呼び出されます。 レイヤーは、受信パスでのパケットの再構築と、送信パスでのパケットの断片化の後に呼び出されます。 これらのレイヤーには、NDIS ライトウェイトフィルター (LWF) ドライバーからアクセスします。

> [!NOTE]
> コールアウトでは、レイヤーに対応するフィルターがまだない場合、そのレイヤーにパケットを挿入することはできません。 [ネットワーク\_バッファー\_リスト](net-buffer-list-structure.md)構造の挿入は、フィルターの追加と削除に合わせて調整し、対応するレイヤーにフィルターが存在する場合にのみ挿入が実行されるようにする必要があります。 また、他のプロバイダーに属しているフィルターを削除することはできません。 

ここでは、次のトピックについて説明します。

-   [MAC フレームの挿入](#injecting-mac-frames)
-   [チェーン化されたネットワークバッファーの一覧の分類](#classifying-chained-network-buffer-lists)
-   [WFP レイヤー2のレイヤーとフィールド](#wfp-layer-2-layers-and-fields)

## <a name="injecting-mac-frames"></a>MAC フレームの挿入

コールバックドライバーは、 [**FwpsInjectMacReceiveAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectmacreceiveasync0)関数を呼び出して、以前に reinject されていた mac フレーム (またはフレームの複製) を、傍受されたレイヤー2の受信データパスに戻すか、または受信データパスに考案済みの mac フレームを挿入します。

コールバックドライバーは、 [**FwpsInjectMacSendAsync0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsinjectmacsendasync0)関数を呼び出して、以前に reinject されていた mac フレーム (またはフレームの複製) を、傍受されたレイヤー2の送信データパスに戻すか、または送信データパスに考案済みの mac フレームを挿入します。

*NetBufferLists*パラメーターには、 [NET\_BUFFER\_LIST](net-buffer-list-structure.md)チェーンを指定できます。 ただし、完了関数は、各チェーンのセグメント (または1つの NET\_バッファー\_リスト) を完了するために複数回呼び出すことができます。

パケットが最初に分類したものと同じフィルターに一致する場合、挿入されたフレームは再び分類される可能性があります。 したがって、IP レイヤーのコールアウトと同様に、レイヤー2のコールアウトは[**FwpsQueryPacketInjectionState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsquerypacketinjectionstate0)を呼び出すことによって無限のパケットインスペクションからも保護する必要があります。

また、を挿入するレイヤーにコールアウトが必要です。 それ以外の場合は、挿入された[net\_buffer\_list](net-buffer-list-structure.md)は完了関数に対して完了しません。また、NET\_BUFFER\_リストがスタックの上に表示されます。 この場合、NDIS は、挿入された NET\_BUFFER\_リストをスタック内の次のコンポーネントに渡そうとします。そのため、動作は定義されていません。

[NET\_BUFFER\_LIST](net-buffer-list-structure.md)**status**メンバーには、スタックインジェクションの状態の結果が含まれています。 スタック挿入の状態の結果は、WFP 挿入関数によって**status\_SUCCESS**が返された後に、スタックによって NET\_BUFFER\_の一覧に格納される状態です。 **NT\_SUCCESS**マクロを使用して、 **status**メンバーのスタック挿入の状態を確認する必要があります。 **状態**の値が [**成功]\_[成功**] の場合、挿入は成功しました。これ以上の情報はありません。 状態 **\_[成功**] よりも大きい**状態**のメンバー値は、挿入が成功したことを意味しますが、考慮する必要がある挿入に関する詳細情報が含まれている可能性があります。 Status **\_SUCCESS**よりも小さい**状態**のメンバー値は、 **status**メンバーに指定された理由で挿入が失敗したことを意味します。

## <a name="classifying-chained-network-buffer-lists"></a>チェーン化されたネットワークバッファーの一覧の分類

既定では、コールアウトドライバーはネットワークバッファーの一覧を個別に分類することしかできません。 ただし、次の両方が実行されている場合は、パフォーマンスを向上させるために、コールアウトドライバーで[NET\_BUFFER\_LIST](net-buffer-list-structure.md)チェーンを分類できます。

-   [**Fwps\_CALLOUT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout2_)構造体の**Flags**メンバーで **\_L2\_BATCH\_分類フラグ\_許可する、\_吹き出し\_フラグ**を指定します。
-   [\_バッファー\_リスト](net-buffer-list-structure.md)チェーンを分類できる[*classifyFn2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn2)関数を登録します。

> [!WARNING]
> ただし、コールアウトドライバーで**FWP_CALLOUT_FLAG_ALLOW_L2_BATCH_CLASSIFY**フラグが設定されている場合、次の関数を使用して NET_BUFFER_LISTs を変更することはできません。
> 
> - [FwpsReferenceNetBufferList0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsreferencenetbufferlist0)
> - [FwpsDereferenceNetBufferList0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsdereferencenetbufferlist0)
> - [FwpsAllocateCloneNetBufferList0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsallocateclonenetbufferlist0)
> - [FwpsFreeCloneNetBufferList0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsfreeclonenetbufferlist0)
>
> このフラグが設定されている場合、 **FwpsAllocateCloneNetBufferList0**は常に**INVALID_PARAMETER**エラーを返します。 これにより、サードパーティのコールアウトドライバーが、NET\_バッファー\_リストの参照カウントを管理できなくなり、送信および受信操作が停止する原因となることがあります。

## <a name="wfp-layer-2-layers-and-fields"></a>WFP レイヤー2のレイヤーとフィールド

仮想スイッチフィルターのランタイムフィルターレイヤー識別子には次のものがあります。

**FWPS\_レイヤー\_受信\_MAC\_フレーム\_イーサネット**

**FWPS\_レイヤー\_送信\_MAC\_フレーム\_イーサネット**

**FWPS\_レイヤー\_受信\_MAC\_フレーム\_ネイティブ**

**FWPS\_レイヤー\_送信\_MAC\_フレーム\_ネイティブ**

仮想スイッチフィルターのデータフィールド識別子には次のものがあります。

[**FWPS\_のフィールド\_受信\_MAC\_フレーム\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_ethernet_)

[**FWPS\_のフィールド\_送信\_MAC\_フレーム\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_ethernet_)

[**FWPS\_のフィールド\_受信\_MAC\_フレーム\_ネイティブ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_native_)

[**FWPS\_のフィールド\_送信\_MAC\_フレーム\_ネイティブ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_native_)

 

 





