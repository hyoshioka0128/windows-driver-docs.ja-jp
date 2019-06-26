---
title: IDebugAdvanced2 要求メソッド
description: 要求メソッドは、さまざまな操作を実行します。
ms.assetid: efb3c93c-5405-418b-a063-afa8e5e9e59a
keywords:
- 要求メソッドが Windows のデバッグ
- Windows デバッグ、IDebugAdvanced2 インターフェイス メソッドを要求します。
- Windows デバッグ、要求メソッド IDebugAdvanced2 インターフェイス
- Windows デバッグ、IDebugAdvanced3 インターフェイス メソッドを要求します。
- Windows デバッグ、要求メソッド IDebugAdvanced3 インターフェイス
topic_type:
- apiref
api_name:
- IDebugAdvanced2.Request
- IDebugAdvanced3.Request
api_location:
- dbgeng.h
api_type:
- COM
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 523f1c29b974531d62984e36fc82e7db8544c2ab
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393110"
---
# <a name="idebugadvanced2request-method"></a>IDebugAdvanced2::Request メソッド


**要求**メソッドは、さまざまな操作を実行します。

<a name="syntax"></a>構文
------

```cpp
HRESULT Request(
  [in]            ULONG  Request,
  [in, optional]  PVOID  InBuffer,
  [in]            ULONG  InBufferSize,
  [out, optional] PVOID  OutBuffer,
  [in]            ULONG  OutBufferSize,
  [out, optional] PULONG OutSize
);
```

<a name="parameters"></a>パラメーター
----------

*要求*\[で\]  
実行する操作を指定します。 **要求**次の表の値のいずれかを指定できます。 「要求」列のリンクに従って、各操作の詳細を確認できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">要求</th>
<th align="left">アクション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="debug-request-source-path-has-source-server.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_SOURCE_PATH_HAS_SOURCE_SERVER&lt;/strong&gt;](debug-request-source-path-has-source-server.md)"><strong>DEBUG_REQUEST_SOURCE_PATH_HAS_SOURCE_SERVER</strong></a></p></td>
<td align="left"><p>移行元サーバーのソース パスを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-target-exception-context.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT&lt;/strong&gt;](debug-request-target-exception-context.md)"><strong>DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT</strong></a></p></td>
<td align="left"><p>返す、<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/scopes-and-symbol-groups#thread-context" data-raw-source="[thread context](https://docs.microsoft.com/windows-hardware/drivers/debugger/scopes-and-symbol-groups#thread-context)">スレッド コンテキスト</a>ユーザー モードのミニダンプ ファイル ストアド イベント。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-target-exception-thread.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_EXCEPTION_THREAD&lt;/strong&gt;](debug-request-target-exception-thread.md)"><strong>DEBUG_REQUEST_TARGET_EXCEPTION_THREAD</strong></a></p></td>
<td align="left"><p>ユーザー モードのミニダンプ ファイル ストアド イベントのオペレーティング システム スレッド ID を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-target-exception-record.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_EXCEPTION_RECORD&lt;/strong&gt;](debug-request-target-exception-record.md)"><strong>DEBUG_REQUEST_TARGET_EXCEPTION_RECORD</strong></a></p></td>
<td align="left"><p>ユーザー モードのミニダンプ ファイルには、ストアド イベントの例外レコードを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-get-additional-create-options.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS&lt;/strong&gt;](debug-request-get-additional-create-options.md)"><strong>DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS</strong></a></p></td>
<td align="left"><p>既定のプロセスの作成オプションを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-set-additional-create-options.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS&lt;/strong&gt;](debug-request-set-additional-create-options.md)"><strong>DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS</strong></a></p></td>
<td align="left"><p>既定のプロセス作成のオプションを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-get-win32-major-minor-versions.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_GET_WIN32_MAJOR_MINOR_VERSIONS&lt;/strong&gt;](debug-request-get-win32-major-minor-versions.md)"><strong>DEBUG_REQUEST_GET_WIN32_MAJOR_MINOR_VERSIONS</strong></a></p></td>
<td align="left"><p>現在、ターゲットで実行されている Windows のバージョンを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff541575(v=vs.85)" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_READ_USER_MINIDUMP_STREAM&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff541575(v=vs.85))"><strong>DEBUG_REQUEST_READ_USER_MINIDUMP_STREAM</strong></a></p></td>
<td align="left"><p>ユーザー モードのミニダンプ ターゲットからストリームを読み取り。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-target-can-detach.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_CAN_DETACH&lt;/strong&gt;](debug-request-target-can-detach.md)"><strong>DEBUG_REQUEST_TARGET_CAN_DETACH</strong></a></p></td>
<td align="left"><p>(実行中のプロセスを離れることが不要になったデバッグされている) 現在のプロセスからデタッチするデバッガー エンジン可能かどうかを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-set-local-implicit-command-line.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE&lt;/strong&gt;](debug-request-set-local-implicit-command-line.md)"><strong>DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE</strong></a></p></td>
<td align="left"><p>設定、<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction#debugger-engine" data-raw-source="[debugger engine](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction#debugger-engine)">デバッガー エンジン</a>の暗黙的なコマンドライン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-get-captured-event-code-offset.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_GET_CAPTURED_EVENT_CODE_OFFSET&lt;/strong&gt;](debug-request-get-captured-event-code-offset.md)"><strong>DEBUG_REQUEST_GET_CAPTURED_EVENT_CODE_OFFSET</strong></a></p></td>
<td align="left"><p>現在のイベントの命令ポインターを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-read-captured-event-code-stream.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_READ_CAPTURED_EVENT_CODE_STREAM&lt;/strong&gt;](debug-request-read-captured-event-code-stream.md)"><strong>DEBUG_REQUEST_READ_CAPTURED_EVENT_CODE_STREAM</strong></a></p></td>
<td align="left"><p>現在のイベントの命令ポインターのメモリの最大 64 バイトを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-ext-typed-data-ansi.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_EXT_TYPED_DATA_ANSI&lt;/strong&gt;](debug-request-ext-typed-data-ansi.md)"><strong>DEBUG_REQUEST_EXT_TYPED_DATA_ANSI</strong></a></p></td>
<td align="left"><p>型指定されたデータの解釈では、さまざまな役立つさまざまな操作を実行します。</p></td>
</tr>
</tbody>
</table>

 

*InBuffer* \[で、省略可能\]  
このメソッドへの入力を指定します。 型と、入力の解釈に依存、*要求*パラメーター。

*受信バッファー サイズ*\[で\]  
入力バッファーのサイズを示す*InBuffer*します。 場合は、要求には、入力は必要ありません*受信バッファー サイズ*0 に設定する必要があります。

*OutBuffer* \[アウト、省略可能\]  
このメソッドから出力を受信します。 型と出力の解釈に依存、*要求*パラメーター。 場合*OutBuffer*は**NULL**出力は返されません。

*送信バッファー サイズ*\[で\]  
出力バッファーのサイズを示す*送信バッファー サイズ*します。 出力の種類が返される場合*OutBuffer*既知のサイズが、*送信バッファー サイズ*場合でも、そのサイズに正確にあると想定されます通常*OutBuffer* に設定されている**NULL**します。

*OutSize* \[アウト、省略可能\]  
出力バッファーに返された出力のサイズを受け取る*OutBuffer*します。 場合*OutSize*は**NULL**、この情報は返されません。

<a name="return-value"></a>戻り値
------------

戻り値の解釈の値によって異なります、*要求*パラメーター。 特に記載がない限り、次の値が返される可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">リターン コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>S_OK</strong></td>
<td align="left"><p>メソッドが正常に完了しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>S_FALSE</strong></td>
<td align="left"><p>メソッドが正常に完了しました。 ただし、出力も適合しない出力バッファーに<em>OutBuffer</em>のため、切り捨てられた出力が返されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>E_INVALIDARG</strong></td>
<td align="left"><p>入力バッファーのサイズ<em>受信バッファー サイズ</em>または出力バッファーのサイズ<em>送信バッファー サイズ</em>が予期される値ではありません。</p></td>
</tr>
</tbody>
</table>

 

このメソッドは、エラー値を返すも可能性があります。 参照してください[**戻り値**](https://docs.microsoft.com/windows-hardware/drivers/debugger/hresult-values)の詳細。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Dbgeng.h (Dbgeng.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**IDebugAdvanced2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugadvanced2)

[**IDebugAdvanced3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugadvanced3)

[**デバッグ\_要求\_ソース\_パス\_HAS\_ソース\_サーバー**](debug-request-source-path-has-source-server.md)

[**デバッグ\_要求\_ターゲット\_例外\_コンテキスト**](debug-request-target-exception-context.md)

[**デバッグ\_要求\_ターゲット\_例外\_スレッド**](debug-request-target-exception-thread.md)

[**デバッグ\_要求\_ターゲット\_例外\_レコード**](debug-request-target-exception-record.md)

[**デバッグ\_要求\_取得\_追加\_作成\_オプション**](debug-request-get-additional-create-options.md)

[**デバッグ\_要求\_設定\_追加\_作成\_オプション**](debug-request-set-additional-create-options.md)

[**デバッグ\_要求\_取得\_WIN32\_メジャー\_マイナー\_バージョン**](debug-request-get-win32-major-minor-versions.md)

[**デバッグ\_要求\_読み取り\_ユーザー\_ミニダンプ\_ストリーム**](https://docs.microsoft.com/previous-versions/ff541575(v=vs.85))

[**デバッグ\_要求\_ターゲット\_できます\_デタッチ**](debug-request-target-can-detach.md)

[**デバッグ\_要求\_設定\_ローカル\_暗黙的\_コマンド\_行**](debug-request-set-local-implicit-command-line.md)

[**デバッグ\_要求\_取得\_CAPTURED\_イベント\_コード\_オフセット**](debug-request-get-captured-event-code-offset.md)

[**デバッグ\_要求\_読み取り\_CAPTURED\_イベント\_コード\_ストリーム**](debug-request-read-captured-event-code-stream.md)

 

 






