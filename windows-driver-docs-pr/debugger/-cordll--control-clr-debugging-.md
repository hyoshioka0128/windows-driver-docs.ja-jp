---
title: .cordll (CLR デバッグの制御)
description: .Cordll コマンド コントロールは、コードのデバッグと Microsoft .NET 共通言語ランタイム (CLR) を管理します。
ms.assetid: d46965b3-4f20-4e25-82e6-79e7fb9b4838
keywords:
- CLR デバッグ (.cordll) コマンドを制御します。
- CLR (共通言語ランタイム)
- .cordll (コントロールの CLR のデバッグ) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .cordll (Control CLR Debugging)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 74b60e1a937d8f14f0e5a8188afbcf532077c330
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572745"
---
# <a name="cordll-control-clr-debugging"></a>.cordll (CLR デバッグの制御)


**.Cordll**コマンド コントロールはマネージ コードのデバッグと Microsoft .NET 共通言語ランタイム (CLR)。

```dbgsyntax
.cordll [Options]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
1 つまたは複数の次のオプション:

<span id="-l___lower-case_L_"></span><span id="-l___lower-case_l_"></span><span id="-L___LOWER-CASE_L_"></span>**-l** (小文字の L)  
CLR モジュールのデバッグを読み込みます。

<span id="-I_Module___upper-case_i__"></span><span id="-i_module___upper-case_i__"></span><span id="-I_MODULE___UPPER-CASE_I__"></span>**-I** **** *モジュール*(大文字の i)   
名前またはデバッグする CLR モジュールのベース アドレスを指定します。 詳細については、「解説」を参照してください。

<span id="-u"></span><span id="-U"></span>**-u**  
モジュールのデバッグ、CLR をアンロードします。

<span id="-e"></span><span id="-E"></span>**-e**  
CLR のデバッグを有効にします。

<span id="-d"></span><span id="-D"></span>**-d**  
CLR のデバッグを無効にします。

<span id="-D"></span><span id="-d"></span>**-D**  
CLR のデバッグを無効にし、CLR デバッグ モジュールをアンロードします。

<span id="-N"></span><span id="-n"></span>**-N**  
CLR モジュールのデバッグを再読み込みします。

<span id="-lp_Path"></span><span id="-lp_path"></span><span id="-LP_PATH"></span>**-lp** **** *パス*  
CLR モジュールのデバッグのディレクトリ パスを指定します。

<span id="-se"></span><span id="-SE"></span>**s**  
CLR モジュールのデバッグの短い名前を使用できるように mscordacwks.dll します。

<span id="-sd"></span><span id="-SD"></span>**-sd**  
CLR モジュールのデバッグの短い名前を使用できないように mscordacwks.dll します。 デバッガーが、CLR デバッグ モジュール mscordacwks の長い名前を使用する代わりに、\_&lt;仕様&gt;.dll です。 短い名前の使用状況をオフにするには、不一致について懸念する場合に使用される、ローカルの CLR を回避することができます。

<span id="-ve"></span><span id="-VE"></span>**-ve**  
CLR モジュールの読み込みの詳細モードをオンにします。

<span id="-vd"></span><span id="-VD"></span>**-vd**  
CLR モジュールの読み込みの詳細モードをオフにします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

マネージ アプリケーションをデバッグするには、デバッガーは、アプリケーションが読み込まれている CLR に対応するデータ アクセス コンポーネント (DAC) を読み込む必要があります。 ただし、場合によっては、アプリケーションは 1 つ以上の CLR を読み込みます。 その場合は、使用することができます、**は**パラメーターを指定する DAC をデバッガーに読み込む必要があります。 、Mscorwks.dll の名前は、CLR のバージョン 2 と CLR の version 4 が Clr.dll をという名前です。 次の例では、デバッガーが DAC バージョン 2 (mscorwks) を読み込む必要がありますを指定する方法を示します。

```dbgcmd
.cordll -I mscorwks -lp c:\dacFolder
```

省略した場合、**は**パラメーター、デバッガーは既定では、バージョン 4 を使用します。 たとえば、次の 2 つのコマンドは同等です。

```dbgcmd
.cordll -lp c:\dacFolder
.cordll -I clr -lp c:\dacFolder
```

Sos.dll は、マネージ コードのデバッグに使用されるコンポーネントです。 Windows のツールのデバッグの現在のバージョンでは、任意のバージョンの sos.dll は含まれません。 Sos.dll を取得する方法については、[SOS デバッガー拡張 (sos.dll) を取得する](debugging-managed-code.md#getting-the-sos-debugging-extension)を参照してください。

**.Cordll**コマンドがカーネル モードのデバッグでサポートされています。 ただし、必要なメモリがページインしない限り、このコマンドが機能しません。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[マネージ Windows デバッガーを使用してコードのデバッグ](debugging-managed-code.md)

[Sos デバッガー拡張](https://go.microsoft.com/fwlink/p/?linkid=223345)

 

 






