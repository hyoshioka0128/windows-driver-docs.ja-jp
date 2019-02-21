---
title: FSCTL_QUERY_VOLUME_NUMA_INFO 制御コード
description: FSCTL\_クエリ\_ボリューム\_NUMA\_情報制御コードは、ボリュームの Non-uniform Memory アーキテクチャ (NUMA) ノードの現在のインデックスを検索します。
ms.assetid: ADDA4A8C-0BF3-45F1-AFE5-956CE5D1FC01
keywords:
- FSCTL_QUERY_VOLUME_NUMA_INFO 制御コード インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FSCTL_QUERY_VOLUME_NUMA_INFO
api_location:
- WinIoctl.h
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7ea4fbfe4ce37d4d16c82416d99e80677f83b2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538201"
---
# <a name="fsctlqueryvolumenumainfo-control-code"></a>FSCTL\_クエリ\_ボリューム\_NUMA\_情報制御コード


**FSCTL\_クエリ\_ボリューム\_NUMA\_情報**制御コードは、ボリュームの Non-uniform Memory アーキテクチャ (NUMA) ノードの現在のインデックスを検索します。

この操作を実行するには、呼び出し、 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)関数は次のパラメーター。

```ManagedCPlusPlus
BOOL 
   WINAPI 
   DeviceIoControl( (HANDLE)       hDevice,         
                    (DWORD)        FSCTL_QUERY_VOLUME_NUMA_INFO, // dwIoControlCode
                    (LPDWORD)      lpInBuffer,      // input buffer
                    (DWORD)        nInBufferSize,   // size of input buffer
                    (LPDWORD)      lpOutBuffer,     // output buffer
                    (DWORD)        nOutBufferSize,  // size of output buffer
                    (LPDWORD)      lpBytesReturned, // number of bytes returned
                    (LPOVERLAPPED) lpOverlapped );  // OVERLAPPED structure
```

<a name="parameters"></a>パラメーター
----------

*hDevice* \[で\]  
デバイスへのハンドル。 デバイス ハンドルを取得する呼び出し、 [ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)関数。

これにより、ファイルまたはディレクトリにもデバイスを識別するハンドルこともできます。 この FSCTL には、ファイルまたはディレクトリが含まれているボリュームの NUMA ノードが返されます。

*dwIoControlCode* \[in\]  
操作の制御コード。 使用**FSCTL\_クエリ\_ボリューム\_NUMA\_情報**この操作にします。

*lpInBuffer*   
この操作では使用されません。設定**NULL**

*nInBufferSize* \[in\]  
この操作では使用されません。0 に設定します。

*lpOutBuffer* \[アウト\]  
受け取るバッファーへのポインターを[ **FSCTL\_クエリ\_ボリューム\_NUMA\_情報\_出力**](https://msdn.microsoft.com/library/windows/hardware/mt827087)以外を指定する構造体メモリ アーキテクチャ (NUMA) ボリュームの現在のノード、統一されました。

*nOutBufferSize* \[in\]  
(バイト単位)、出力バッファーのサイズ。

*lpBytesReturned* \[out\]  
(バイト単位)、出力バッファーに格納されているデータのサイズを受け取る変数へのポインター。

出力バッファーが小さすぎる場合は、呼び出しが失敗した、 [ **GetLastError** ](https://msdn.microsoft.com/library/windows/desktop/ms679360)返します**エラー\_不十分\_バッファー**、および*lpBytesReturned*は 0 です。

場合*lpOverlapped*は**NULL**、 *lpBytesReturned*することはできません**NULL**します。 でもときに操作を返しません出力データと*lpOutBuffer*は**NULL**、 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)活用*lpBytesReturned*します。 このような操作の値の後に*lpBytesReturned*は意味がありません。

場合*lpOverlapped*ない**NULL**、 *lpBytesReturned*できる**NULL**します。 このパラメーターがない場合**NULL**操作は、そのデータを返します*lpBytesReturned*オーバー ラップ処理が完了するまでは無意味です。 返されるバイト数を取得する[ **GetOverlappedResult**](https://msdn.microsoft.com/library/windows/desktop/ms683209)します。 場合、 *hDevice*パラメーターは、I/O 完了ポートに関連付け、呼び出すことによって返されるバイト数を取得する[ **GetQueuedCompletionStatus**](https://msdn.microsoft.com/library/windows/desktop/aa364986)します。

*lpOverlapped* \[in\]  
ポインター、 [ **OVERLAPPED** ](https://msdn.microsoft.com/library/windows/desktop/ms684342)構造体。

場合*hDevice*を指定せずに開かれた**ファイル\_フラグ\_OVERLAPPED**、 *lpOverlapped*は無視されます。

場合*hDevice*で開かれた、**ファイル\_フラグ\_OVERLAPPED**フラグは、操作がオーバー ラップ (非同期) 操作として実行します。 この場合、 *lpOverlapped*有効 をポイントする必要があります[ **OVERLAPPED** ](https://msdn.microsoft.com/library/windows/desktop/ms684342)イベント オブジェクトへのハンドルを含む構造体。 それ以外の場合、関数は、予測できない方法で失敗します。

重複した操作は、 [ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)を即座に返します、操作が完了したときに、イベント オブジェクトがシグナル状態とします。 それ以外の場合、操作が完了したか、エラーが発生するまでには、この関数は返されません。

<a name="return-value"></a>戻り値
------------

操作が正常に完了した場合[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216) 0 以外の値を返します。

操作は、障害が発生したり、保留中で[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)は 0 を返します。 拡張エラー情報を取得するには呼び出します[ **GetLastError**](https://msdn.microsoft.com/library/windows/desktop/ms679360)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">WinIoctl.h;Ntifs.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)

[**FSCTL\_クエリ\_ボリューム\_NUMA\_情報\_出力**](https://msdn.microsoft.com/library/windows/hardware/mt827087)

 

 






