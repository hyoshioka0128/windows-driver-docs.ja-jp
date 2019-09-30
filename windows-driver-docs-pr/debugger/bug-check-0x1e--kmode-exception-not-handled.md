---
title: バグチェック 0x1E KMODE_EXCEPTION_NOT_HANDLED
description: KMODE_EXCEPTION_NOT_HANDLED のバグチェックの値は、0x0000001E です。 これは、カーネルモードプログラムが、エラーハンドラーがキャッチしなかった例外を生成したことを示します。
ms.assetid: 4a30b770-b2c4-4fdd-b431-95f2b40ef5f7
keywords:
- バグチェック 0x1E KMODE_EXCEPTION_NOT_HANDLED
- KMODE_EXCEPTION_NOT_HANDLED
ms.date: 08/23/2018
topic_type:
- apiref
api_name:
- KMODE_EXCEPTION_NOT_HANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 12de66c44cafd8e06ceb3277510b447f94052a6a
ms.sourcegitcommit: 667b4be765b2eac6bc586d39abef3393a718b23f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "70025332"
---
# <a name="bug-check-0x1e-kmode_exception_not_handled"></a>バグ チェック 0x1E:KMODE\_EXCEPTION\_NOT\_HANDLED


KMODE @ no__t-0EXCEPTION @ no__t-1NOT @ no__t-2HANDLED バグチェックの値は0x0000001E です。 これは、カーネルモードプログラムが、エラーハンドラーがキャッチしなかった例外を生成したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="kmode_exception_not_handled-parameters"></a>Kmode\_EXCEPTION\_NOT\_HANDLEDのパラメーター


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
<td align="left"><p>例外のパラメーター0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>例外のパラメーター1</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このバグチェックを解釈するには、生成された例外を特定する必要があります。

一般的な例外コードは次のとおりです。

-   0x80000002STATUS\_DATATYPE\_MISALIGNMENT

    整列されていないデータ参照が見つかりました。

-   0x80000003:STATUS\_BREAKPOINT

    カーネルデバッガーがシステムにアタッチされていないときに、ブレークポイントまたはアサートが発生しました。

-   0XC0000005STATUS\_ACCESS\_VIOLATION

    メモリアクセス違反が発生しました。 (バグチェックのパラメーター4は、ドライバーがアクセスしようとしたアドレスです)。

例外コードの完全な一覧については、「 [NTSTATUS 値](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)」を参照してください。 例外コードは、 [Windows Driver Kit](https://docs.microsoft.com/windows-hardware/drivers/)の inc. ディレクトリにある ntstatus ファイルにも記載されています。


<a name="remarks"></a>コメント
----------

**この問題をデバッグする必要がない場合**は、「 [**Blue Screen Data**](blue-screen-data.md)」で説明されている基本的なトラブルシューティング手法を使用できます。 バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

**ハードウェアに互換性がありません**

インストールされている新しいハードウェアに、インストールされている Windows のバージョンとの互換性があることを確認します。 たとえば、 [Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)では、必要なハードウェアに関する情報を取得できます。

**デバイスドライバーまたはシステムサービスに問題があります**

また、障害が発生しているデバイスドライバーまたはシステムサービスがこのエラーの原因となる場合があります。 BIOS の非互換性、メモリの競合、および IRQ の競合などのハードウェアの問題によって、このエラーが発生することもあります。

バグチェックメッセージ内にドライバーが名前で表示されている場合は、そのドライバーを無効にするか削除します。 最近追加されたドライバーまたはサービスをすべて無効にするか削除します。 起動シーケンス中にエラーが発生し、システムパーティションが NTFS ファイルシステムでフォーマットされている場合は、セーフモードを使用してデバイスマネージャーでドライバーを無効にすることができます。

バグチェック0x1E の原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。 また、システムの製造元から提供されているハードウェア診断 (特にメモリスキャナー) を実行する必要もあります。 これらの手順の詳細については、コンピューターの所有者のマニュアルを参照してください。

このメッセージを生成するエラーは、Windows セットアップ中に最初に再起動した後、またはセットアップが完了した後に発生する可能性があります。 このエラーの原因として、システム BIOS との互換性がないことが考えられます。 BIOS の問題は、システムの BIOS のバージョンをアップグレードすることで解決できます。

<a name="resolution"></a>解決方法
----------

**この問題のデバッグを計画している場合**は、スタックトレースを取得するのが困難な場合があります。 パラメーター 2 (例外アドレス) は、この問題の原因となったドライバーまたは機能を特定する必要があります。

例外コード0x80000003 が発生した場合は、ハードコーディングされたブレークポイントまたはアサーションがヒットしたが、システムは **/NODEBUG**スイッチを使用して起動されたことを示します。 この問題はめったに発生しません。 繰り返し発生する場合は、カーネルデバッガーが接続されていて、システムが **/debug**スイッチで起動されていることを確認します。

例外コード0x80000002 が発生した場合、トラップフレームは追加情報を提供します。

例外の特定の原因が不明な場合は、次のことを考慮する必要があります。


**通常のスタックトレースプロシージャが失敗した場合にスタックトレースを取得するには**

1.  [ [**Kb (スタックバックトレースの表示)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) ] コマンドを使用して、スタックトレースにパラメーターを表示します。 NT! の呼び出しを探します **。PspUnhandledExceptionInSystemThread**。 (この関数が表示されない場合は、以下のメモを参照してください)。

2.  NT! の最初のパラメーター **PspUnhandledExceptionInSystemThread**は、 **except**ステートメントへのポインターを含む構造体へのポインターです。

    ```cpp
    typedef struct _EXCEPTION_POINTERS {
        PEXCEPTION_RECORD ExceptionRecord;
        PCONTEXT ContextRecord;
        } EXCEPTION_POINTERS, *PEXCEPTION_POINTERS;

    ULONG PspUnhandledExceptionInSystemThread(
        IN PEXCEPTION_POINTERS ExceptionPointers
        )
    ```

    必要なデータを表示するには、そのアドレスに対して[**dd (Display Memory)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドを使用します。

3.  最初に取得された値は例外レコードで、2番目の値はコンテキストレコードです。 これらの2つの値をそれぞれ引数として使用して、 [ **. exr (表示例外レコード)** ](-exr--display-exception-record-.md)コマンドと、 [**Cxr (表示コンテキストレコード)** ](-cxr--display-context-record-.md)コマンドを使用します。

4.  **Cxr**コマンドを実行した後、 **kb**コマンドを使用して、コンテキストレコード情報に基づくスタックトレースを表示します。 このスタックトレースは、未処理の例外が発生した呼び出し履歴を示します。

**注**  this 手順では、 **NT!PspUnhandledExceptionInSystemThread**。 ただし、場合によっては (アクセス違反のクラッシュなど)、これを行うことはできません。 その場合は、次のようにし**ます。KiDispatchException**。 この関数に渡される3番目のパラメーターは、トラップフレームアドレスです。 このアドレスと共に、[**トラップ (トラップフレームの表示)** ](-trap--display-trap-frame-.md)コマンドを使用して、レジスタコンテキストを適切な値に設定します。 その後、スタックトレースを実行し、他のコマンドを発行できます。

 

X86 プロセッサでのバグチェック0x1E の例を次に示します。

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
