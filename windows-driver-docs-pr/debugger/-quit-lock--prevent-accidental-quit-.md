---
title: .quit_lock (偶発的終了を禁止)
description: .Quit_lock コマンドでは、誤って、デバッグ セッションを終了することを防止するためのパスワードを設定します。
ms.assetid: fd40e642-beba-4da0-a072-6493588980de
keywords:
- .quit_lock (偶発的終了を禁止) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .quit_lock (Prevent Accidental Quit)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a3c975a14ce2adfeabd2604b35c06d1bbb92b629
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559859"
---
# <a name="quitlock-prevent-accidental-quit"></a>.quit\_ロック (ように偶発的な終了)


**.Quit\_ロック**コマンドは、誤って、デバッグ セッションを終了することを防止するためのパスワードを設定します。

```dbgcmd
.quit_lock /s NewPassword 
.quit_lock /q Password 
.quit_lock 
```

## <a name="span-idddkmetapreventaccidentalquitdbgspanspan-idddkmetapreventaccidentalquitdbgspanparameters"></a><span id="ddk_meta_prevent_accidental_quit_dbg"></span><span id="DDK_META_PREVENT_ACCIDENTAL_QUIT_DBG"></span>パラメーター


<span id="________s_NewPassword_____________"></span><span id="________s_newpassword_____________"></span><span id="________S_NEWPASSWORD_____________"></span> **/s** **** *NewPassword*   
により、デバッグ セッションを終了し、格納*NewPassword*します。 使用するまで、デバッガー セッションを終了することはできません、 **.quit\_ロック/q**コマンドと共にこれと同じパスワードです。 *NewPassword*任意の文字列を使用することができます。 囲む必要がありますが、スペースが含まれる場合*NewPassword*引用符で囲んで指定します。

<span id="________q_Password______________"></span><span id="________q_password______________"></span><span id="________Q_PASSWORD______________"></span> **/q** **** *Password*   
デバッグ セッションを終了できるようにします。 *パスワード*で設定したパスワードが一致する必要があります、 **.quit\_ロック/s**コマンド。

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

 

<a name="remarks"></a>注釈
-------

パラメーターを指定せず **.quit\_ロック**パスワードの完全なテキストを含む、現在のロック状態を表示します。

繰り返すことができます、 **.quit\_ロック/s**既存のパスワードを変更するコマンド。

使用すると **.quit\_/q をロック**ロックを削除します。 このコマンドでは、デバッガーは終了しません。 代わりに、コマンドしか有効にする場合に、一般的な方法で、セッションを終了します。

**注**  パスワードに「シークレット」がありません。 デバッグ セッションに関連付けられているすべてのリモート ユーザーが使える **.quit\_ロック**パスワードを特定します。 このコマンドの目的は、偶発的な使用できないようにするのには、 [ **q (終了)** ](q--qq--quit-.md)コマンド。 このコマンドは、デバッグ セッションを再起動できない場合があります (たとえば、リモート デバッグ) 中の場合に特に便利です。

 

使用することはできません、 **.quit\_ロック/s**コマンド[保護モード](activating-secure-mode.md)。 保護モードは、前に、このコマンドを使用する場合、パスワード保護のアクティブ化、ままですが、変更またはパスワードを削除することはできません。

 

 





