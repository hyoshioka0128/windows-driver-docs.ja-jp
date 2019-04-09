---
title: バグ チェック 0x1E KMODE_EXCEPTION_NOT_HANDLED
description: KMODE_EXCEPTION_NOT_HANDLED のバグ チェックでは、0x0000001E の値を持ちます。 これは、カーネル モードのプログラムがエラー ハンドラーをキャッチされなかった例外を生成することを示します。
ms.assetid: 4a30b770-b2c4-4fdd-b431-95f2b40ef5f7
keywords:
- バグ チェック 0x1E KMODE_EXCEPTION_NOT_HANDLED
- KMODE_EXCEPTION_NOT_HANDLED
ms.date: 08/23/2018
topic_type:
- apiref
api_name:
- KMODE_EXCEPTION_NOT_HANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bb5479e33d9e87f4bf6b155ab5535ec0680088a3
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238619"
---
# <a name="bug-check-0x1e-kmodeexceptionnothandled"></a>バグ チェック 0x1E:KMODE\_例外\_いない\_処理済み


KMODE\_例外\_いない\_処理済みのバグ チェックが 0x0000001E の値を持ちます。 これは、カーネル モードのプログラムがエラー ハンドラーをキャッチされなかった例外を生成することを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="kmodeexceptionnothandled-parameters"></a>KMODE\_例外\_いない\_処理済みのパラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>処理されなかった例外コード</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>例外が発生したアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>例外のパラメーター 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>例外のパラメーター 1</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグ チェックを解釈するには、どの例外が発生しましたを識別する必要があります。

一般的な例外コードは次のとおりです。

-   0x80000002:ステータス\_DATATYPE\_不整合

    アラインされていないデータの参照が発生しました。

-   0x80000003:ステータス\_ブレークポイント

    システムにカーネル デバッガーが関連付けられていない場合、ブレークポイントまたはアサートが発生しました。

-   0xC0000005:ステータス\_アクセス\_違反

    メモリ アクセス違反が発生しました。 (パラメーター 4 のバグ チェックは、ドライバーにアクセスしようとするアドレスです)。

例外コードの完全な一覧を参照してください。 [NTSTATUS 値](https://msdn.microsoft.com/library/cc704588.aspx)します。 例外コードは、の inc ディレクトリにある ntstatus.h ファイルにも表示されます、 [Windows Driver Kit](https://docs.microsoft.com/windows-hardware/drivers/)します。


<a name="remarks"></a>注釈
----------

**この問題をデバッグする装備していない場合**で説明されている基本的なトラブルシューティングの手法を使用する[**青い画面データ**](blue-screen-data.md)します。 バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

**ハードウェアの互換性がないです。**

インストールされている新しいハードウェアが Windows のインストールされているバージョンと互換性があることを確認します。 たとえばに必要なハードウェアに関する情報を取得できます[Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)します。

**障害のあるデバイス ドライバーまたはシステム サービス**

さらに、障害のあるデバイス ドライバーまたはシステム サービスは、このエラーを担当する可能性があります。 BIOS の非互換性、メモリの競合および IRQ の競合などのハードウェアの問題には、このエラーを生成できます。

バグ チェック メッセージ内で名前によってドライバーがある場合は、無効にするか、またはそのドライバーを削除します。 無効にするか、または、ドライバーや最近追加されたサービスを削除します。 起動シーケンス中にエラーが発生し、システム パーティションが NTFS ファイル システムでフォーマットされたの場合は、セーフ モードを使用して、デバイス マネージャーでのドライバーを無効にすることができます。

デバイスまたは 0x1E のバグ チェックが原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。 システム製造元から提供されたハードウェア診断が特にメモリ スキャナーを実行することもあります。 詳細については、これらの手順は、コンピューターの製造元のマニュアルを参照してください。

このメッセージを生成するエラーは、最初の再起動後、Windows セットアップ中に、またはセットアップの完了後に発生します。 エラーの考えられる原因は、システム BIOS の非互換性です。 システム BIOS のバージョンをアップグレードすることで、BIOS の問題を解決できます。

<a name="resolution"></a>解決方法
----------

**この問題をデバッグする予定の場合**、スタック トレースを取得する困難な見つけることがあります。 (例外のアドレス) を 2 番目のパラメーターには、ドライバーまたはこの問題の原因となった関数を特定する必要があります。

アサーション、ハード コーディングされたブレークポイントにヒットしますが、システムで開始されたことを示しますこの例外コード 0x80000003 が発生した場合、 **/NODEBUG**スイッチします。 この問題が発生することはほとんどありません必要があります。 これが繰り返し発生する場合、カーネル デバッガーが接続されているし、システムを起動すると、 **/debug**スイッチします。

例外コード 0x80000002 が発生した場合、トラップ フレームは追加情報を提供します。

例外の具体的な原因が不明な場合、次の検討してください。


**通常のスタック トレースのプロシージャが失敗する場合は、スタック トレースを取得するには**

1.  使用して、 [ **kb (Stack Backtrace の表示)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)スタック トレース内のパラメーターを表示するコマンド。 呼び出しを探して**NT!PspUnhandledExceptionInSystemThread**します。 (この関数が表示されない場合参照下記の注を参照)。

2.  最初のパラメーター **NT!PspUnhandledExceptionInSystemThread**へのポインターを含む構造体へのポインター、**を除く**ステートメント。

    ```cpp
    typedef struct _EXCEPTION_POINTERS {
        PEXCEPTION_RECORD ExceptionRecord;
        PCONTEXT ContextRecord;
        } EXCEPTION_POINTERS, *PEXCEPTION_POINTERS;

    ULONG PspUnhandledExceptionInSystemThread(
        IN PEXCEPTION_POINTERS ExceptionPointers
        )
    ```

    使用して、 [ **dd (メモリの表示)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドに必要なデータを表示するには、そのアドレスをします。

3.  取得した最初の値は例外レコードで、2 番目はコンテキスト レコードです。 使用して、 [ **.exr (例外レコードの表示)** ](-exr--display-exception-record-.md)コマンドと[ **.cxr (コンテキスト レコードの表示)** ](-cxr--display-context-record-.md)とこれら 2 つの値を持つコマンドその引数では、それぞれします。

4.  後に、 **.cxr**を実行するコマンドを使用して、 **kb**コンテキスト レコードの情報に基づいているスタック トレースを表示するコマンド。 このスタック トレースでは、コール スタックがハンドルされない例外が発生したことを示します。

**注**  を特定できることが前提と**NT!PspUnhandledExceptionInSystemThread**します。 ただし、場合によっては (アクセス違反クラッシュの場合) などをできなくこれを行う。 その場合は、探して**ntoskrnl!KiDispatchException**します。 この関数に渡される 3 番目のパラメーターは、トラップ フレームのアドレスです。 使用して、 [ **.trap (表示トラップ フレーム)** ](-trap--display-trap-frame-.md)登録コンテキストを適切な値に設定するには、このアドレスを持つコマンド。 スタック トレースを実行し、その他のコマンドを発行できます。

 

X86 のバグ チェック 0x1E の例を次に示しますプロセッサ。

```dbgcmd
kd> .bugcheck                 get the bug check data
Bugcheck code 0000001e
Arguments c0000005 8013cd0a 00000000 0362cffff

kd> kb                        start with a stack trace 
FramePtr  RetAddr   Param1   Param2   Param3   Function Name 
8013ed5c  801263ba  00000000 00000000 fe40cb00 NT!_DbgBreakPoint 
8013eecc  8013313c  0000001e c0000005 8013cd0a NT!_KeBugCheckEx+0x194
fe40cad0  8013318e  fe40caf8 801359ff fe40cb00 NT!PspUnhandledExceptionInSystemThread+0x18
fe40cad8  801359ff  fe40cb00 00000000 fe40cb00 NT!PspSystemThreadStartup+0x4a
fe40cf7c  8013cb8e  fe43a44c ff6ce388 00000000 NT!_except_handler3+0x47
00000000  00000000  00000000 00000000 00000000 NT!KiThreadStartup+0xe

kd> dd fe40caf8 L2            dump EXCEPTION_POINTERS structure
0xFE40CAF8  fe40cd88 fe40cbc4                   ..@...@.

kd> .exr fe40cd88             first DWORD is the exception record
Exception Record @ FE40CD88:
   ExceptionCode: c0000005
  ExceptionFlags: 00000000
  Chained Record: 00000000
ExceptionAddress: 8013cd0a
NumberParameters: 00000002
   Parameter[0]: 00000000
   Parameter[1]: 0362cfff

kd> .cxr fe40cbc4             second DWORD is the context record
CtxFlags: 00010017
eax=00087000 ebx=00000000 ecx=03ff0000 edx=ff63d000 esi=0362cfff edi=036b3fff
eip=8013cd0a esp=fe40ce50 ebp=fe40cef8 iopl=0         nv dn ei pl nz ac po cy
vip=0    vif=0
cs=0008  ss=0010  ds=0023  es=0023  fs=0030  gs=0000             efl=00010617
0x8013cd0a  f3a4             rep movsb

kd> kb                        kb gives stack for context record
ChildEBP RetAddr  Args to Child
fe40ce54 80402e09 ff6c4000 ff63d000 03ff0000 NT!_RtlMoveMemory@12+0x3e
fe40ce68 80403c18 ffbc0c28 ff6ce008 ff6c4000 HAL!_HalpCopyBufferMap@20+0x49
fe40ce9c fe43b1e4 ff6cef90 ffbc0c28 ff6ce009 HAL!_IoFlushAdapterBuffers@24+0x148
fe40ceb8 fe4385b4 ff6ce388 6cd00800 ffbc0c28 QIC117!_kdi_FlushDMABuffers@20+0x28
fe40cef8 fe439894 ff6cd008 ffb6c820 fe40cf4c QIC117!_cqd_CmdReadWrite@8+0x26e
fe40cf18 fe437d92 ff6cd008 ffb6c820 ff6e4e50 QIC117!_cqd_DispatchFRB@8+0x210
fe40cf30 fe43a4f5 ff6cd008 ffb6c820 00000000 QIC117!_cqd_ProcessFRB@8+0x134
fe40cf4c 80133184 ff6ce388 00000000 00000000 QIC117!_kdi_ThreadRun@4+0xa9
fe40cf7c 8013cb8e fe43a44c ff6ce388 00000000 NT!_PspSystemThreadStartup@8+0x40
```

**旅行時間のトレース**

バグ チェックはオンデマンドで再現できる場合は、WinDbg のプレビューを使用してタイム トラベル トレースを取ることの可能性を調査します。 詳細については、次を参照してください。[タイム トラベルのデバッグ - 概要](time-travel-debugging-overview.md)します。

 




