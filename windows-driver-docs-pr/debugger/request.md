---
title: IDebugAdvanced2 Request メソッド
description: 要求メソッドは、さまざまな操作を実行します。
ms.assetid: efb3c93c-5405-418b-a063-afa8e5e9e59a
keywords:
- 要求メソッド Windows デバッグ
- Request メソッド Windows デバッグ、IDebugAdvanced2 インターフェイス
- IDebugAdvanced2 インターフェイス Windows デバッグ、要求メソッド
- Request メソッド Windows デバッグ、IDebugAdvanced3 インターフェイス
- IDebugAdvanced3 インターフェイス Windows デバッグ、要求メソッド
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
ms.openlocfilehash: ceb843ea83c9aa22b85805f06e37a57de7c45b45
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834277"
---
# <a name="idebugadvanced2request-method"></a>IDebugAdvanced2:: Request メソッド


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

\] での \[*要求*  
実行する操作を指定します。 **要求**は、次の表のいずれかの値を指定できます。 各操作の詳細については、「Request」列のリンクを参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">要求</th>
<th align="left">[操作]</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="debug-request-source-path-has-source-server.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_SOURCE_PATH_HAS_SOURCE_SERVER&lt;/strong&gt;](debug-request-source-path-has-source-server.md)"><strong>DEBUG_REQUEST_SOURCE_PATH_HAS_SOURCE_SERVER</strong></a></p></td>
<td align="left"><p>ソースサーバーのソースパスを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-target-exception-context.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT&lt;/strong&gt;](debug-request-target-exception-context.md)"><strong>DEBUG_REQUEST_TARGET_EXCEPTION_CONTEXT</strong></a></p></td>
<td align="left"><p>ユーザーモードのミニダンプファイルに格納されているイベントの<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/scopes-and-symbol-groups#thread-context" data-raw-source="[thread context](https://docs.microsoft.com/windows-hardware/drivers/debugger/scopes-and-symbol-groups#thread-context)">スレッドコンテキスト</a>を返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-target-exception-thread.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_EXCEPTION_THREAD&lt;/strong&gt;](debug-request-target-exception-thread.md)"><strong>DEBUG_REQUEST_TARGET_EXCEPTION_THREAD</strong></a></p></td>
<td align="left"><p>ユーザーモードのミニダンプファイルに格納されているイベントのオペレーティングシステムのスレッド ID を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-target-exception-record.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_EXCEPTION_RECORD&lt;/strong&gt;](debug-request-target-exception-record.md)"><strong>DEBUG_REQUEST_TARGET_EXCEPTION_RECORD</strong></a></p></td>
<td align="left"><p>ユーザーモードのミニダンプファイルに格納されているイベントの例外レコードを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-get-additional-create-options.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS&lt;/strong&gt;](debug-request-get-additional-create-options.md)"><strong>DEBUG_REQUEST_GET_ADDITIONAL_CREATE_OPTIONS</strong></a></p></td>
<td align="left"><p>既定のプロセス作成オプションを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-set-additional-create-options.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS&lt;/strong&gt;](debug-request-set-additional-create-options.md)"><strong>DEBUG_REQUEST_SET_ADDITIONAL_CREATE_OPTIONS</strong></a></p></td>
<td align="left"><p>既定のプロセス作成オプションを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-get-win32-major-minor-versions.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_GET_WIN32_MAJOR_MINOR_VERSIONS&lt;/strong&gt;](debug-request-get-win32-major-minor-versions.md)"><strong>DEBUG_REQUEST_GET_WIN32_MAJOR_MINOR_VERSIONS</strong></a></p></td>
<td align="left"><p>ターゲットで現在実行されている Windows のバージョンを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff541575(v=vs.85)" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_READ_USER_MINIDUMP_STREAM&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff541575(v=vs.85))"><strong>DEBUG_REQUEST_READ_USER_MINIDUMP_STREAM</strong></a></p></td>
<td align="left"><p>ユーザーモードのミニダンプターゲットからストリームを読み取ります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-target-can-detach.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_TARGET_CAN_DETACH&lt;/strong&gt;](debug-request-target-can-detach.md)"><strong>DEBUG_REQUEST_TARGET_CAN_DETACH</strong></a></p></td>
<td align="left"><p>デバッガーエンジンが現在のプロセスからデタッチされる可能性があるかどうかを確認します (プロセスは実行されていますが、デバッグされなくなっています)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-set-local-implicit-command-line.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE&lt;/strong&gt;](debug-request-set-local-implicit-command-line.md)"><strong>DEBUG_REQUEST_SET_LOCAL_IMPLICIT_COMMAND_LINE</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction#debugger-engine" data-raw-source="[debugger engine](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction#debugger-engine)">デバッガーエンジン</a>の暗黙のコマンドラインを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-get-captured-event-code-offset.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_GET_CAPTURED_EVENT_CODE_OFFSET&lt;/strong&gt;](debug-request-get-captured-event-code-offset.md)"><strong>DEBUG_REQUEST_GET_CAPTURED_EVENT_CODE_OFFSET</strong></a></p></td>
<td align="left"><p>現在のイベントの命令ポインターを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-request-read-captured-event-code-stream.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_READ_CAPTURED_EVENT_CODE_STREAM&lt;/strong&gt;](debug-request-read-captured-event-code-stream.md)"><strong>DEBUG_REQUEST_READ_CAPTURED_EVENT_CODE_STREAM</strong></a></p></td>
<td align="left"><p>現在のイベントの命令ポインターで最大64バイトのメモリを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-request-ext-typed-data-ansi.md" data-raw-source="[&lt;strong&gt;DEBUG_REQUEST_EXT_TYPED_DATA_ANSI&lt;/strong&gt;](debug-request-ext-typed-data-ansi.md)"><strong>DEBUG_REQUEST_EXT_TYPED_DATA_ANSI</strong></a></p></td>
<td align="left"><p>型指定されたデータの解釈に役立つさまざまな操作を実行します。</p></td>
</tr>
</tbody>
</table>

 

*Inbuffer* \[、オプション\]  
このメソッドへの入力を指定します。 入力の型と解釈は、*要求*パラメーターによって異なります。

*Inbuffersize* \[\]  
入力バッファーのサイズを指定し*ます。* 要求に入力が不要な場合は、 *Inbuffersize*を0に設定する必要があります。

*Outbuffer* \[out、省略可能\]  
このメソッドからの出力を受け取ります。 出力の型と解釈は、*要求*パラメーターによって異なります。 *Outbuffer*が**NULL**の場合、出力は返されません。

\] の*Outbuffersize* \[  
出力バッファーのサイズを*指定します*。 *Outbuffer に返さ*れる出力の型に既知のサイズが指定されている場合、 *Outbuffer*が**NULL**に設定されていても、通常、 *outbuffer*はそのサイズと正確に一致している必要があります。

*Outsize* \[out、省略可能\]  
出力バッファー *outbuffer*で返された出力のサイズを受け取ります。 *Outsize*が**NULL**の場合、この情報は返されません。

<a name="return-value"></a>戻り値
------------

戻り値の解釈は、*要求*パラメーターの値によって異なります。 特に明記されていない限り、次の値が返される可能性があります。

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
<td align="left"><p>メソッドが正常に実行されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>S_FALSE</strong></td>
<td align="left"><p>メソッドが正常に実行されました。 ただし、出力は出力バッファーの<em>Outbuffer</em>に収まりません。そのため、切り捨てられた出力が返されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>E_INVALIDARG</strong></td>
<td align="left"><p>入力バッファーのサイズ、または出力バッファー <em>Outbuffersize</em>のサイズが予期された値<em>ではあり</em>ませんでした。</p></td>
</tr>
</tbody>
</table>

 

このメソッドは、エラー値を返す場合もあります。 詳細については、「[**戻り値**](https://docs.microsoft.com/windows-hardware/drivers/debugger/hresult-values)」を参照してください。

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
<td align="left">Dbgeng .h (Dbgeng .h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**IDebugAdvanced2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced2)

[**IDebugAdvanced3**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced3)

[**デバッグ\_要求\_ソース\_パス\_に\_ソース\_サーバーがある**](debug-request-source-path-has-source-server.md)

[**デバッグ\_要求\_ターゲット\_例外\_コンテキスト**](debug-request-target-exception-context.md)

[**デバッグ\_要求\_ターゲット\_例外\_スレッド**](debug-request-target-exception-thread.md)

[**デバッグ\_要求\_ターゲット\_例外\_レコード**](debug-request-target-exception-record.md)

[**デバッグ\_要求\_追加\_\_オプションを作成\_** ](debug-request-get-additional-create-options.md)

[**デバッグ\_要求\_設定\_追加\_\_オプションを作成する**](debug-request-set-additional-create-options.md)

[**デバッグ\_要求\_WIN32\_メジャー\_マイナー\_バージョン\_取得する**](debug-request-get-win32-major-minor-versions.md)

[**デバッグ\_要求\_読み取り\_ユーザー\_ミニダンプ\_ストリーム**](https://docs.microsoft.com/previous-versions/ff541575(v=vs.85))

[**デバッグ\_要求\_ターゲット\_をデタッチ\_ことができます**](debug-request-target-can-detach.md)

[**デバッグ\_要求\_ローカル\_暗黙的\_コマンド\_行\_設定します**](debug-request-set-local-implicit-command-line.md)

[**デバッグ\_要求\_取得\_\_キャプチャされたイベント\_コード\_オフセット**](debug-request-get-captured-event-code-offset.md)

[**デバッグ\_要求\_読み取り\_キャプチャされた\_イベント\_コード\_ストリーム**](debug-request-read-captured-event-code-stream.md)

 

 






