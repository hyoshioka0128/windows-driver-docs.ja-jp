---
title: .cordll (CLR デバッグの制御)
description: Cordll コマンドは、マネージコードデバッグと Microsoft .NET 共通言語ランタイム (CLR) を制御します。
ms.assetid: d46965b3-4f20-4e25-82e6-79e7fb9b4838
keywords:
- CLR デバッグの制御 (cordll) コマンド
- CLR (共通言語ランタイム)
- cordll (CLR デバッグの制御) Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .cordll (Control CLR Debugging)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 174b7bea404ef5240d74d16f5403cd60ac1e28e4
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534239"
---
# <a name="cordll-control-clr-debugging"></a>.cordll (CLR デバッグの制御)

**Cordll**コマンドは、マネージコードデバッグと Microsoft .NET 共通言語ランタイム (CLR) を制御します。

```dbgsyntax
.cordll [Options]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*オプション*   
次のオプションの1つまたは複数です。

<span id="-l___lower-case_L_"></span><span id="-l___lower-case_l_"></span><span id="-L___LOWER-CASE_L_"></span>**-l** (小文字の l)  
CLR デバッグモジュールを読み込みます。

<span id="-I_Module___upper-case_i__"></span><span id="-i_module___upper-case_i__"></span><span id="-I_MODULE___UPPER-CASE_I__"></span>**-I**  **** *モジュール*(大文字)   
デバッグする CLR モジュールの名前またはベースアドレスを指定します。 詳細については、「解説」を参照してください。

<span id="-u"></span><span id="-U"></span>**-u**  
CLR デバッグモジュールをアンロードします。

<span id="-e"></span><span id="-E"></span>**-e**  
CLR デバッグを有効にします。

<span id="-d"></span><span id="-D"></span>**-d.ddd...e**  
CLR デバッグを無効にします。

<span id="-D"></span><span id="-d"></span>**-D**  
CLR デバッグを無効にし、CLR デバッグモジュールをアンロードします。

<span id="-N"></span><span id="-n"></span>**-N**  
CLR デバッグモジュールを再読み込みします。

<span id="-lp_Path"></span><span id="-lp_path"></span><span id="-LP_PATH"></span>**-lp**  **** *パス*  
CLR デバッグモジュールのディレクトリパスを指定します。

<span id="-se"></span><span id="-SE"></span>**-se**  
CLR デバッグモジュール (mscordacwks) の短い名前を使用できるようにします。

<span id="-sd"></span><span id="-SD"></span>**-sd**  
CLR デバッグモジュール (mscordacwks) の短い名前の使用を無効にします。 代わりに、デバッガーは CLR デバッグモジュール mscordacwks の長い名前を使用し \_ &lt; &gt; ます。 短い名前の使用を無効にすると、不一致が懸念される場合に、ローカル CLR を使用しないようにすることができます。

<span id="-ve"></span><span id="-VE"></span>**-ve**  
CLR モジュール読み込みの詳細モードをオンにします。

<span id="-vd"></span><span id="-VD"></span>**-vd**  
CLR モジュール読み込みの詳細モードをオフにします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>Environment

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザーモード、カーネルモード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべて</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

マネージアプリケーションをデバッグするには、アプリケーションが読み込んだ CLR に対応するデータアクセスコンポーネント (DAC) をデバッガーで読み込む必要があります。 ただし、場合によっては、アプリケーションが複数の CLR を読み込むことがあります。 その場合は、 **I**パラメーターを使用して、デバッガーが読み込む DAC を指定できます。 CLR のバージョン2には Mscorwks.dll という名前が付けられ、CLR のバージョン4は Clr という名前になります。 次の例は、デバッガーがバージョン 2 (mscorwks.dll) の DAC を読み込むように指定する方法を示しています。

```dbgcmd
.cordll -I mscorwks -lp c:\dacFolder
```

**I**パラメーターを省略した場合、デバッガーは既定でバージョン4を使用します。 たとえば、次の2つのコマンドは同等です。

```dbgcmd
.cordll -lp c:\dacFolder
.cordll -I clr -lp c:\dacFolder
```

Sos はマネージコードのデバッグに使用されるコンポーネントです。 Windows 用デバッグツールの現在のバージョンには、どのバージョンの sos .dll も含まれていません。 Sos を取得する方法の詳細については、「 [Windows デバッガーを使用したマネージコードのデバッグ](debugging-managed-code.md)」の「 *sos デバッガー拡張 (Sos) の取得*」を参照してください。

**Cordll**コマンドは、カーネルモードのデバッグでサポートされています。 ただし、必要なメモリがページングされていないと、このコマンドは動作しない可能性があります。

## <a name="see-also"></a>こちらもご覧ください

[Windows デバッガーを使用したマネージド コードのデバッグ](debugging-managed-code.md)

[SOS デバッガー拡張機能](https://docs.microsoft.com/dotnet/framework/tools/sos-dll-sos-debugging-extension)
