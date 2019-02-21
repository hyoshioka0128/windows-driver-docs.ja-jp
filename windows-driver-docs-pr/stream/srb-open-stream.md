---
title: SRB\_オープン\_ストリーム
description: SRB\_オープン\_ストリーム
ms.assetid: 53732add-e304-4128-9235-525ff073d777
keywords:
- SRB_OPEN_STREAM ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_OPEN_STREAM
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cd03dfbc3e5784ecbda3f3a93486d412ba9ada8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530103"
---
# <a name="srbopenstream"></a>SRB\_オープン\_ストリーム


## <span id="ddk_srb_open_stream_ks"></span><span id="DDK_SRB_OPEN_STREAM_KS"></span>


クラス ドライバーは、ストリームを開くには、この要求を送信します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
コマンドが正常に完了を示します。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>ステータス\_いない\_実装されていません  
関数が、ミニドライバーでサポートされていないことを示します。

<span id="STATUS_TOO_MANY_NODES"></span><span id="status_too_many_nodes"></span>ステータス\_すぎます\_多く\_ノード  
このストリームを開くには、十分なリソースがないことを示します。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>ステータス\_IO\_デバイス\_エラー  
ハードウェア障害が発生したことを示します。

### <a name="comments"></a>コメント

クラス ドライバーを提供する[ **HW\_ストリーム\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff559697)内でバッファー *pSrb* - &gt; **StreamObject**で*pSrb*-&gt;**StreamObject**-&gt;**StreamNumber**に開かれるストリームの数に設定します。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff559702)構造体。 **StreamNumber**内のストリームのオフセットに対応する、 [ **HW\_ストリーム\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff559686) への応答で、ミニドライバーは、構造体[**SRB\_取得\_ストリーム\_情報**](srb-get-stream-info.md)要求。 クラスのドライバーで開いているストリームを提供するデータ形式を指定する*pSrb*-&gt;**CommandData** - &gt; **OpenFormat**します。

ミニドライバーは、この要求を受信したときに、この時点で、指定したストリームを開くことができるかどうかそれを判断する必要があります。 ミニドライバーを確認することも、 [ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)で形式が渡されます。 SRB の OpenFormat フィールドです。 ストリームを開くには場合、ミニドライバーは、ハードウェアを更新\_ストリーム\_オブジェクトの構造、および状態を返します。\_成功します。 開いているストリーム インスタンスの最大数、またはこのストリームを開くために必要なハードウェア リソースが使用可能な、ミニドライバーは、該当するエラー状態を返します。

**ときに、SRB\_オープン\_ミニドライバーがストリームのコマンドを受信した、ようにミニドライバーにする必要があります。**

1.  ストリームのインスタンスの最大数が超過したいないことと、ストリームのインデックス値が有効であるを確認します。

2.  要求されたデータの形式がこのストリームの有効なことを確認します。

3.  ストリームの形式を設定します。

4.  任意のストリームから Irp をキャンセルできるように、デバイスの拡張機能ですべてのストリーム拡張機能の構造の配列を維持します。

5.  ストリームのデータ ハンドラーとコントロール ハンドラーに、ストリーム オブジェクトにポインターを指定します。

6.  渡されたデータ バッファーのアドレスの場合は、デバイスでは、DMA に直接実行はストリームの DMA フラグのオブジェクト セット、 **ReceiveDataPacket**ルーチン。 ドライバーが論理アドレスを使用して渡されたデータ バッファーにアクセスする場合は、ストリーム オブジェクトで PIO フラグを設定もします。

7.  ストリームでクロックのサポートが利用可能な場合でこれを示す、 **HwClockObject**ストリーム オブジェクト内のメンバー。

 

 





