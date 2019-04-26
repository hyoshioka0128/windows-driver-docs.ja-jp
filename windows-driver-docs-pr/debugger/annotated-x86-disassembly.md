---
title: 注釈付き x86 逆アセンブリ
description: 注釈付き x86 逆アセンブリ
ms.assetid: ea1e67c8-d752-42d8-92db-a0c105ceddd6
keywords:
- x86 プロセッサ、注釈付き逆アセンブリ
- x86 プロセッサ、アセンブリ コード
- x86 プロセッサ、ソース コード
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6ffc922683f13ddbb2c4de0523439e3b9cb8a95
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346350"
---
# <a name="annotated-x86-disassembly"></a>注釈付き x86 逆アセンブリ


## <span id="ddk_annotated_x86_disassembly_dbg"></span><span id="DDK_ANNOTATED_X86_DISASSEMBLY_DBG"></span>


次のセクションでは逆アセンブリ例説明をします。

### <a name="span-idsourcecodespanspan-idsourcecodespanspan-idsourcecodespansource-code"></a><span id="Source_Code"></span><span id="source_code"></span><span id="SOURCE_CODE"></span>ソース コード

分析される関数のコードを次に示します。

```cpp
HRESULT CUserView::CloseView(void)
{
    if (m_fDestroyed) return S_OK;

    BOOL fViewObjectChanged = FALSE;
    ReleaseAndNull(&m_pdtgt);

    if (m_psv) {
        m_psb->EnableModelessSB(FALSE);
        if(m_pws) m_pws->ViewReleased();

        IShellView* psv;

        HWND hwndCapture = GetCapture();
        if (hwndCapture && hwndCapture == m_hwnd) {
            SendMessage(m_hwnd, WM_CANCELMODE, 0, 0);
        }

        m_fHandsOff = TRUE;
        m_fRecursing = TRUE;
        NotifyClients(m_psv, NOTIFY_CLOSING);
        m_fRecursing = FALSE;

        m_psv->UIActivate(SVUIA_DEACTIVATE);

        psv = m_psv;
        m_psv = NULL;

        ReleaseAndNull(&_pctView);

        if (m_pvo) {
            IAdviseSink *pSink;
            if (SUCCEEDED(m_pvo->GetAdvise(NULL, NULL, &pSink)) && pSink) {
                if (pSink == (IAdviseSink *)this)
                    m_pvo->SetAdvise(0, 0, NULL);
                pSink->Release();
            }

            fViewObjectChanged = TRUE;
            ReleaseAndNull(&m_pvo);
        }

        if (psv) {
            psv->SaveViewState();
            psv->DestroyViewWindow();
            psv->Release();
        }

        m_hwndView = NULL;
        m_fHandsOff = FALSE;

        if (m_pcache) {
            GlobalFree(m_pcache);
            m_pcache = NULL;
        }

        m_psb->EnableModelessSB(TRUE);

        CancelPendingActions();
    }

    ReleaseAndNull(&_psf);

    if (fViewObjectChanged)
        NotifyViewClients(DVASPECT_CONTENT, -1);

    if (m_pszTitle) {
        LocalFree(m_pszTitle);
        m_pszTitle = NULL;
    }

    SetRect(&m_rcBounds, 0, 0, 0, 0);
    return S_OK;
}
```

### <a name="span-idassemblycodespanspan-idassemblycodespanspan-idassemblycodespanassembly-code"></a><span id="Assembly_Code"></span><span id="assembly_code"></span><span id="ASSEMBLY_CODE"></span>アセンブリ コード

このセクションには、注釈付き逆アセンブリの使用例が含まれています。

関数を使用する、 **ebp**フレーム ポインターが次のようにまずとして登録します。

```dbgcmd
HRESULT CUserView::CloseView(void)
SAMPLE!CUserView__CloseView:
71517134 55               push    ebp
71517135 8bec             mov     ebp,esp
```

関数からのオフセットを正の値としてそのパラメーターにアクセスできるように、フレームを設定この**ebp**、およびローカル変数として負のオフセット。

呼び出し規則が、このメソッドは、プライベートの COM インターフェイスでメソッド **\_ \_stdcall**します。 つまり、パラメーターを左に直接プッシュされます (この場合が含まれていない)、"this"ポインターがプッシュされるし、関数が呼び出されます。 したがって、関数には、入力時にスタックの次に示します。

```dbgcmd
[esp+0] = return address
[esp+4] = this
```

2 つの前の手順の後に、パラメーターとしてアクセス可能です。

```dbgcmd
[ebp+0] = previous ebp pushed on stack
[ebp+4] = return address
[ebp+8] = this
```

使用する関数の**ebp**フレーム ポインターとして最初にプッシュされたパラメーターがでアクセス可能\[ **ebp**+8\]それ以降のパラメーターが以上連続でアクセス可能DWORD のアドレス。

```dbgcmd
71517137 51               push    ecx
71517138 51               push    ecx
```

この関数がそのためだけの 2 つのローカル スタック変数を必要と、 **esp を sub**, 8 命令。 プッシュされた値は、として利用できます\[ **ebp**-4\]と\[ **ebp**-8\]します。

使用する関数の**ebp**フレーム ポインターとしてスタックのローカル変数はから負のオフセット位置にアクセスできる、 **ebp**を登録します。

```dbgcmd
71517139 56               push    esi
```

今すぐ、コンパイラは、関数呼び出し間で保持するために必要なレジスタを保存します。 実際には、その実際のコードの最初の行と交互に配置されている各種に保存します。

```dbgcmd
7151713a 8b7508           mov     esi,[ebp+0x8]     ; esi = this
7151713d 57               push    edi               ; save another registers
```

Closeview ユーティリティが ViewState、つまり基になるオブジェクト内のオフセット 12 時のメソッドであるため発生します。 その結果、**この**別の基本クラスで混乱がある場合は、としてはより慎重に指定されますが、ViewState クラスへのポインターは、(ViewState\*)**この**します。

```dbgcmd
    if (m_fDestroyed)
7151713e 33ff             xor     edi,edi           ; edi = 0
```

隠ぺい自体の登録は、アウトされ、ゼロイングの標準的な方法です。

```dbgcmd
71517140 39beac000000     cmp     [esi+0xac],edi    ; this->m_fDestroyed == 0?
71517146 7407             jz      NotDestroyed (7151714f)  ; jump if equal
```

**Cmp**命令 (減算) を 2 つの値を比較します。 **Jz**命令は、2 つが値を比較することを示すが等しい場合は、結果がゼロを確認します。

Cmp 命令は、2 つの値を比較します。比較の結果に基づいてジャンプ後続 j 命令。

```dbgcmd
    return S_OK;
71517148 33c0             xor     eax,eax           ; eax = 0 = S_OK
7151714a e972010000       jmp     ReturnNoEBX (715172c1) ; return, do not pop EBX
```

関数で後で、EBX レジスタの保存の遅延コンパイラのためプログラムがこのテストは、終了パス上の"初期 out"になる場合必要がありますいる EBX は復元されません。

```dbgcmd
    BOOL fViewObjectChanged = FALSE;
    ReleaseAndNull(&m_pdtgt);
```

これらの 2 行のコードの実行をインターリーブ、ので注意してください。

```dbgcmd
NotDestroyed:
7151714f 8d86c0000000     lea     eax,[esi+0xc0]    ; eax = &m_pdtgt
```

**元に戻せる**命令のメモリ アクセスの効果アドレスを計算し、変換先に格納されます。 実際のメモリ アドレスが逆参照しないでください。

元に戻せる命令は、変数のアドレスを取得します。

```dbgcmd
71517155 53               push    ebx
```

破損している前に、その EBX レジスタを保存する必要があります。

```dbgcmd
71517156 8b1d10195071     mov ebx,[_imp__ReleaseAndNull]
```

呼び出すため、 **ReleaseAndNull** EBX でそのアドレスをキャッシュすることをお勧めは多くの場合、します。

```dbgcmd
7151715c 50               push    eax               ; parameter to ReleaseAndNull
7151715d 897dfc           mov     [ebp-0x4],edi     ; fViewObjectChanged = FALSE
71517160 ffd3             call    ebx               ; call ReleaseAndNull
    if (m_psv) {
71517162 397e74           cmp     [esi+0x74],edi    ; this->m_psv == 0?
71517165 0f8411010000     je      No_Psv (7151727c) ; jump if zero
```

元に戻すに EDI レジスタをゼロすること、および EDI 関数呼び出しにわたって維持レジスタに注意してください (そのためへの呼び出し**ReleaseAndNull**変更しなかった)。 したがって、値 0 をそのまま保持され、0 をすばやくテストを使用することができます。

```dbgcmd
        m_psb->EnableModelessSB(FALSE);
7151716b 8b4638           mov     eax,[esi+0x38]    ; eax = this->m_psb
7151716e 57               push    edi               ; FALSE
7151716f 50               push    eax               ; "this" for callee
71517170 8b08             mov     ecx,[eax]         ; ecx = m_psb->lpVtbl
71517172 ff5124           call    [ecx+0x24]        ; __stdcall EnableModelessSB
```

上記のパターンは、COM メソッドの呼び出しの証拠となります。

COM メソッドの呼び出しは、認識されるようにする方法を説明するので、非常に好評です。 具体的には、3 つの IUnknown メソッドが Vtable から直接のオフセットを認識できる必要があります。QueryInterface = 0、AddRef = 4、およびリリース = 8。

```dbgcmd
        if(m_pws) m_pws->ViewReleased();
71517175 8b8614010000     mov     eax,[esi+0x114]   ; eax = this->m_pws
7151717b 3bc7             cmp     eax,edi           ; eax == 0?
7151717d 7406             jz      NoWS (71517185) ; if so, then jump
7151717f 8b08             mov     ecx,[eax]         ; ecx = m_pws->lpVtbl
71517181 50               push    eax               ; "this" for callee
71517182 ff510c           call    [ecx+0xc]         ; __stdcall ViewReleased
NoWS:
        HWND hwndCapture = GetCapture();
71517185 ff15e01a5071    call [_imp__GetCapture]    ; call GetCapture
```

グローバル変数を通じて間接的な呼び出しは、Microsoft Win32 の関数インポートを実装する方法です。 ローダーは、ターゲットの実際のアドレスを指定する、グローバル変数を修正します。 これは、クラッシュしたマシンを調査している場合は、状況を取得する便利な方法です。 インポートされた関数に移動して、ターゲットでの通話を探します。 通常、ソース コードであるかを判断するために使用できるいくつかのインポート関数の名前があります。

```dbgcmd
        if (hwndCapture && hwndCapture == m_hwnd) {
            SendMessage(m_hwnd, WM_CANCELMODE, 0, 0);
        }
7151718b 3bc7             cmp     eax,edi           ; hwndCapture == 0?
7151718d 7412             jz      No_Capture (715171a1) ; jump if zero
```

戻り値は、EAX に、関数を登録します。

```dbgcmd
7151718f 8b4e44           mov     ecx,[esi+0x44]    ; ecx = this->m_hwnd
71517192 3bc1             cmp     eax,ecx           ; hwndCapture = ecx?
71517194 750b             jnz     No_Capture (715171a1) ; jump if not

71517196 57               push    edi               ; 0
71517197 57               push    edi               ; 0
71517198 6a1f             push    0x1f              ; WM_CANCELMODE
7151719a 51               push    ecx               ; hwndCapture
7151719b ff1518195071     call    [_imp__SendMessageW] ; SendMessage
No_Capture:
        m_fHandsOff = TRUE;
        m_fRecursing = TRUE;
715171a1 66818e0c0100000180 or    word ptr [esi+0x10c],0x8001 ; set both flags at once

        NotifyClients(m_psv, NOTIFY_CLOSING);
715171aa 8b4e20           mov     ecx,[esi+0x20]    ; ecx = (CNotifySource*)this.vtbl
715171ad 6a04             push    0x4               ; NOTIFY_CLOSING
715171af 8d4620           lea     eax,[esi+0x20]    ; eax = (CNotifySource*)this
715171b2 ff7674           push    [esi+0x74]        ; m_psv
715171b5 50               push    eax               ; "this" for callee
715171b6 ff510c           call    [ecx+0xc]         ; __stdcall NotifyClients
```

別の基本クラスから独自のメソッドを呼び出すときに、"this"ポインターを変更する必要があった方法に注意してください。

```dbgcmd
        m_fRecursing = FALSE;
715171b9 80a60d0100007f   and     byte ptr [esi+0x10d],0x7f
        m_psv->UIActivate(SVUIA_DEACTIVATE);
715171c0 8b4674           mov     eax,[esi+0x74]    ; eax = m_psv
715171c3 57               push    edi               ; SVUIA_DEACTIVATE = 0
715171c4 50               push    eax               ; "this" for callee
715171c5 8b08             mov     ecx,[eax]         ; ecx = vtbl
715171c7 ff511c           call    [ecx+0x1c]        ; __stdcall UIActivate
        psv = m_psv;
        m_psv = NULL;
715171ca 8b4674           mov     eax,[esi+0x74]    ; eax = m_psv
715171cd 897e74           mov     [esi+0x74],edi    ; m_psv = NULL
715171d0 8945f8           mov     [ebp-0x8],eax     ; psv = eax
```

最初のローカル変数は**psv**します。

```dbgcmd
        ReleaseAndNull(&_pctView);
715171d3 8d466c           lea     eax,[esi+0x6c]    ; eax = &_pctView
715171d6 50               push    eax               ; parameter
715171d7 ffd3             call    ebx               ; call ReleaseAndNull
        if (m_pvo) {
715171d9 8b86a8000000     mov     eax,[esi+0xa8]    ; eax = m_pvo
715171df 8dbea8000000     lea     edi,[esi+0xa8]    ; edi = &m_pvo
715171e5 85c0             test    eax,eax           ; eax == 0?
715171e7 7448             jz      No_Pvo (71517231) ; jump if zero
```

コンパイラは、のアドレスを投機的準備に注意してください、 **m\_pvo**メンバー、しばらくの間の頻繁に使用するためです。 そのため、便利なアドレスを持つより小さなコードされます。

```dbgcmd
            if (SUCCEEDED(m_pvo->GetAdvise(NULL, NULL, &pSink)) && pSink) {
715171e9 8b08             mov     ecx,[eax]         ; ecx = m_pvo->lpVtbl
715171eb 8d5508           lea     edx,[ebp+0x8]     ; edx = &pSink
715171ee 52               push    edx               ; parameter
715171ef 6a00             push    0x0               ; NULL
715171f1 6a00             push    0x0               ; NULL
715171f3 50               push    eax               ; "this" for callee
715171f4 ff5120           call    [ecx+0x20]        ; __stdcall GetAdvise
715171f7 85c0             test    eax,eax           ; test bits of eax
715171f9 7c2c             jl      No_Advise (71517227) ; jump if less than zero
715171fb 33c9             xor     ecx,ecx           ; ecx = 0
715171fd 394d08           cmp     [ebp+0x8],ecx     ; _pSink == ecx?
71517200 7425             jz      No_Advise (71517227)
```

コンパイラという結論に達しましたを受信"this"パラメーターありません必要な (ESI レジスタに格納される前) のために注意してください。 そのため、ローカル変数 pSink としてメモリに再利用します。

関数は、EBP フレームを使用する場合は、EBP から受信パラメーターが正の値のオフセット位置に到達し、ローカル変数は、負のオフセットに配置します。 ただし、この場合は、のように、コンパイラが自由に目的を問わずそのメモリを再利用します。

細心の注意を支払いする場合は、コンパイラをもう少しよくこのコードが最適化が表示されます。 遅れてでした、**元に戻せる edi、 \[esi + 0xa8\]**  、2 つが終了するまで命令**0x0 をプッシュ**手順については、それらを置き換える**ediプッシュ**. これは、2 バイトを保存したは。

```dbgcmd
                if (pSink == (IAdviseSink *)this)
```

これらの次の数行が C++ ことで、ファクトを補正するためには (IAdviseSink \*)**NULL**する必要がある**NULL**します。 実際には、"this の"もし"(ViewState\*) NULL"、キャストの結果になりますし、 **NULL** IAdviseSink と IBrowserService 間の距離ではありません。

```dbgcmd
71517202 8d46ec           lea     eax,[esi-0x14]    ; eax = -(IAdviseSink*)this
71517205 8d5614           lea     edx,[esi+0x14]    ; edx = (IAdviseSink*)this
71517208 f7d8             neg     eax               ; eax = -eax (sets carry if != 0)
7151720a 1bc0             sbb     eax,eax           ; eax = eax - eax - carry
7151720c 23c2             and     eax,edx           ; eax = NULL or edx
```

条件付き移動命令を Pentium には、基本 i386 アーキテクチャは使用できない、コンパイラでは、具体的な技法を使用して、任意のジャンプすることがなく条件付き移動命令をシミュレートするため。

条件付き評価のための一般的なパターンは次のです。

```dbgcmd
        neg     r
        sbb     r, r
        and     r, (val1 - val2)
        add     r, val2
```

**Neg r**場合は、キャリー フラグを設定**r** 0 以外の場合、ため**neg**ゼロから差し引くことで値を否定します。 0 以外の値を減算する場合、0 から減算すると、borrow (set やし) が生成するされます。 値を破損することも、 **r**レジスタをそれが許容される上書きしようとしているためです。

次に、 **sbb r、r**命令は常に 0 になりますが、それ自体から値を減算します。 ただし、やし関数も (借用) ビット、最終的に設定するのには、 **r** 0 または-1 の場合は、やしがあったかどうかに応じてまたはオフにそれぞれ設定します。

そのため、 **sbb r、r**設定**r**場合は 0 に、元の値の**r**が 0、または元の値がゼロ以外にする場合は-1。

3 番目の命令では、マスクを実行します。 **R**レジスタは、0 または-1、"this"機能のままにするか**r**ゼロまたは変更する**r** -1 から **(val1 - val1)** 点で、and 演算任意の値に-1 は、元の値を残します。

結果ではそのため、"と、r (val1 - val1)"に設定する r 0 r の元の値が 0、または"(val1 - val2)"を r の元の値がゼロ以外の場合。

最後に、追加**val2**に**r**で結果として得られる、 **val2**または **(val1 - val2) + val2 = val1**します。

したがって、この一連の命令の最終的な結果は設定を**r**に**val2** 0 の場合、またはに**val1** 0 以外の場合。 これは、アセンブリと同等の**r = r? val1: val2**します。

この特定のインスタンスにすることがわかります**val2 = 0**と**val1 = (IAdviseSink\*) この**します。 (通知、コンパイラが、最終的なを省略**eax、0 を追加**命令効果があるないためです)。

```dbgcmd
7151720e 394508           cmp     [ebp+0x8],eax ; pSink == (IAdviseSink*)this?
71517211 750b             jnz     No_SetAdvise (7151721e) ; jump if not equal
```

以前、このセクションで設定した EDI のアドレスに、 **m\_pvo**メンバー。 これで、使用しようとは。 前に ECX レジスタをゼロもします。

```dbgcmd
                    m_pvo->SetAdvise(0, 0, NULL);
71517213 8b07             mov     eax,[edi]         ; eax = m_pvo
71517215 51               push    ecx               ; NULL
71517216 51               push    ecx               ; 0
71517217 51               push    ecx               ; 0
71517218 8b10             mov     edx,[eax]         ; edx = m_pvo->lpVtbl
7151721a 50               push    eax               ; "this" for callee
7151721b ff521c           call    [edx+0x1c]        ; __stdcall SetAdvise
No_SetAdvise:
                pSink->Release();
7151721e 8b4508           mov     eax,[ebp+0x8]     ; eax = pSink
71517221 50               push    eax               ; "this" for callee
71517222 8b08             mov     ecx,[eax]         ; ecx = pSink->lpVtbl
71517224 ff5108           call    [ecx+0x8]         ; __stdcall Release
No_Advise:
```

これらすべての COM メソッド呼び出しの使用率は見覚えがあります。

次の 2 つのステートメントの評価はインターリーブされます。 EBX にはアドレスが含まれている必ず**ReleaseAndNull**します。

```dbgcmd
            fViewObjectChanged = TRUE;
            ReleaseAndNull(&m_pvo);
71517227 57               push    edi               ; &m_pvo
71517228 c745fc01000000   mov     dword ptr [ebp-0x4],0x1 ; fViewObjectChanged = TRUE
7151722f ffd3             call    ebx               ; call ReleaseAndNull
No_Pvo:
        if (psv) {
71517231 8b7df8           mov     edi,[ebp-0x8]     ; edi = psv
71517234 85ff             test    edi,edi           ; edi == 0?
71517236 7412             jz      No_Psv2 (7151724a) ; jump if zero
            psv->SaveViewState();
71517238 8b07             mov     eax,[edi]         ; eax = psv->lpVtbl
7151723a 57               push    edi               ; "this" for callee
7151723b ff5034           call    [eax+0x34]        ; __stdcall SaveViewState
```

ここより多くの COM メソッド呼び出しです。

```dbgcmd
            psv->DestroyViewWindow();
7151723e 8b07             mov     eax,[edi]         ; eax = psv->lpVtbl
71517240 57               push    edi               ; "this" for callee
71517241 ff5028           call    [eax+0x28]        ; __stdcall DestroyViewWindow
            psv->Release();
71517244 8b07             mov     eax,[edi]         ; eax = psv->lpVtbl
71517246 57               push    edi               ; "this" for callee
71517247 ff5008           call    [eax+0x8]         ; __stdcall Release
No_Psv2:
        m_hwndView = NULL;
7151724a 83667c00         and     dword ptr [esi+0x7c],0x0 ; m_hwndView = 0
```

And 演算のゼロ メモリの場所は、0 に設定した場合と同じため、何も 0 は 0。 相当するものより大幅に短くなって場合でも、低速であるため、コンパイラはこのフォームを使用して**mov**命令。 (このコードは、サイズ、速度ではなく用に最適化された)。

```dbgcmd
        m_fHandsOff = FALSE;
7151724e 83a60c010000fe   and     dword ptr [esi+0x10c],0xfe
        if (m_pcache) {
71517255 8b4670           mov     eax,[esi+0x70]    ; eax = m_pcache
71517258 85c0             test    eax,eax           ; eax == 0?
7151725a 740b             jz      No_Cache (71517267) ; jump if zero
            GlobalFree(m_pcache);
7151725c 50               push    eax               ; m_pcache
7151725d ff15b4135071     call    [_imp__GlobalFree]    ; call GlobalFree
            m_pcache = NULL;
71517263 83667000         and     dword ptr [esi+0x70],0x0 ; m_pcache = 0
No_Cache:
        m_psb->EnableModelessSB(TRUE);
71517267 8b4638           mov     eax,[esi+0x38]    ; eax = this->m_psb
7151726a 6a01             push    0x1               ; TRUE
7151726c 50               push    eax               ; "this" for callee
7151726d 8b08             mov     ecx,[eax]         ; ecx = m_psb->lpVtbl
7151726f ff5124           call    [ecx+0x24]        ; __stdcall EnableModelessSB
        CancelPendingActions();
```

呼び出すために**CancelPendingActions**から移動する必要が (ViewState\*) これを (CUserView\*) これです。 また、 **CancelPendingActions**を使用して、 \_ \_thiscall の呼び出し規約の代わりに\_ \_stdcall します。 に従って\_ \_thiscall、"this"ポインターが渡されるスタックに渡されるのではなく、ECX レジスタにします。

```dbgcmd
71517272 8d4eec           lea     ecx,[esi-0x14]    ; ecx = (CUserView*)this
71517275 e832fbffff       call CUserView::CancelPendingActions (71516dac) ; __thiscall
    ReleaseAndNull(&_psf);
7151727a 33ff             xor     edi,edi           ; edi = 0 (for later)
No_Psv:
7151727c 8d4678           lea     eax,[esi+0x78]    ; eax = &_psf
7151727f 50               push    eax               ; parameter
71517280 ffd3             call    ebx               ; call ReleaseAndNull
    if (fViewObjectChanged)
71517282 397dfc           cmp     [ebp-0x4],edi     ; fViewObjectChanged == 0?
71517285 740d             jz      NoNotifyViewClients (71517294) ; jump if zero
       NotifyViewClients(DVASPECT_CONTENT, -1);
71517287 8b46ec           mov     eax,[esi-0x14]    ; eax = ((CUserView*)this)->lpVtbl
7151728a 8d4eec           lea     ecx,[esi-0x14]    ; ecx = (CUserView*)this
7151728d 6aff             push    0xff              ; -1
7151728f 6a01             push    0x1               ; DVASPECT_CONTENT = 1
71517291 ff5024           call    [eax+0x24]        ; __thiscall NotifyViewClients
NoNotifyViewClients:
    if (m_pszTitle)
71517294 8b8680000000     mov     eax,[esi+0x80]    ; eax = m_pszTitle
7151729a 8d9e80000000     lea     ebx,[esi+0x80]    ; ebx = &m_pszTitle (for later)
715172a0 3bc7             cmp     eax,edi           ; eax == 0?
715172a2 7409             jz      No_Title (715172ad) ; jump if zero
        LocalFree(m_pszTitle);
715172a4 50               push    eax               ; m_pszTitle
715172a5 ff1538125071     call   [_imp__LocalFree]
        m_pszTitle = NULL;
```

EDI が 0 のままと、EBX、(& m) 静止\_pszTitle、これらのレジスタが関数呼び出しによって保持されるため、します。

```dbgcmd
715172ab 893b             mov     [ebx],edi         ; m_pszTitle = 0
No_Title:
    SetRect(&m_rcBounds, 0, 0, 0, 0);
715172ad 57               push    edi               ; 0
715172ae 57               push    edi               ; 0
715172af 57               push    edi               ; 0
715172b0 81c6fc000000     add     esi,0xfc          ; esi = &this->m_rcBounds
715172b6 57               push    edi               ; 0
715172b7 56               push    esi               ; &m_rcBounds
715172b8 ff15e41a5071     call   [_imp__SetRect]
```

注意する必要はありません"this"の値かどうかをコンパイラが使用するため、**追加**命令アドレスを保持する別のレジスタを使用する代わりにインプレース変更します。 これは、実際に Pentium u/v パイプライン処理、v パイプは、算術演算を実行できますが、計算を示さないためによりパフォーマンス勝利です。

```dbgcmd
    return S_OK;
715172be 33c0             xor     eax,eax           ; eax = S_OK
```

最後に、レジスタに保持し、スタックをクリーンアップし、受信パラメーターを削除する、呼び出し元に返す必要がありますを復元します。

```dbgcmd
715172c0 5b               pop     ebx               ; restore
ReturnNoEBX:
715172c1 5f               pop     edi               ; restore
715172c2 5e               pop     esi               ; restore
715172c3 c9               leave                     ; restores EBP and ESP simultaneously
715172c4 c20400           ret     0x4               ; return and clear parameters
```

 

 





