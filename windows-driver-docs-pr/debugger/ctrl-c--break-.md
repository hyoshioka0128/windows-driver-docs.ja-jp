---
title: CTRL + C (中断)
description: Ctrl キーを押しながら C キーは、対象のアプリケーションまたは対象のコンピューターを停止する、デバッガーを中断し、デバッガー コマンドを取り消します。
ms.assetid: ee9df6d7-4a40-4006-90df-478e06899e3a
keywords:
- CTRL + C (中断) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CTRL+C (Break)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 82745fadf91909aad4b85c6760f3012a3eab3b4e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550821"
---
# <a name="ctrlc-break"></a>CTRL + C (中断)


Ctrl キーを押しながら C キーは、対象のアプリケーションまたは対象のコンピューターを停止する、デバッガーを中断し、デバッガー コマンドを取り消します。

CDB 構文

```dbgcmd
CTRL+C 
```

KD 構文

```dbgcmd
CTRL+C 
```

ターゲット コンピューターの構文

```dbgcmd
SYSRQ 
ALT+SYSRQ 
F12 
```

## <span id="ddk_meta_ctrl_c_dbg"></span><span id="DDK_META_CTRL_C_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>デバッガー</strong></p></td>
<td align="left"><p>CDB と KD のみ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

このコマンドと、関連するコマンドの概要を発行するには、他の方法を参照してください。[ターゲットを制御する](controlling-the-target.md)します。

<a name="remarks"></a>注釈
-------

**ときに、CDB を使用します。**

ユーザー モードでは、ctrl キーを押しながら C キーは、デバッガーを中断するターゲット アプリケーションです。 ターゲット アプリケーションがフリーズ、デバッガーがアクティブになり、デバッガー コマンドを入力することができます。

デバッガーが既にアクティブな場合は、CTRL + C では、この対象アプリケーションは影響しません。 これは、デバッガー コマンドを終了するただし、使用するには、ことができます。 たとえば、長い表示を要求したして確認する必要がなくなった場合 CTRL + C は、表示を終了し、デバッガーのコマンド プロンプトに戻ります。

CDB でのリモート デバッグを実行する場合、ホスト コンピューターのキーボードで CTRL キーを押しながら C キーを押すことができます。 ターゲット コンピューターのキーボードからの離別を発行する場合は、CTRL + C を使用して、x86 マシン。

デバッグ中のアプリケーションがビジー状態の場合は、コマンド プロンプトを取得するのには、F12 キーを使用できます。 ターゲット アプリケーションの windows のいずれかにフォーカスを設定し、対象のコンピュータの F12 キーを押します。

**KD を使用する: 場合**

カーネル モードでは、ctrl キーを押しながら C キーは、デバッガーを中断する対象のコンピュータとされます。 これにより、ターゲット コンピューターをロックし、デバッガーを起動します。

実行されているシステム、デバッグ時に、最初のコマンド プロンプトを取得するホスト キーボードの CTRL + C が押さする必要があります。

デバッガーが既にアクティブ、CTRL + C では、対象のコンピュータは影響しません。 使用できます、ただし、デバッガー コマンドを終了します。 たとえば、長い表示を要求したして確認する必要がなくなった場合 CTRL + C は、表示を終了し、デバッガーのコマンド プロンプトに戻ります。

CTRL + C を長いディスプレイやターゲット コンピューターがビジー状態の場合、デバッガー コマンドが生成するときに、コマンド プロンプトを取得することもできます。 X86 をデバッグするときにコンピューター、ホストまたはターゲットのいずれかのキーボードで押されたすることができます。

SYSRQ (または拡張キーボードの ALT + SYSRQ) は似ています。 すべてのプロセッサ上のホストまたはターゲットのキーボード動作します。 ただし、これは、プロンプトがキーを押して CTRL + C を少なくとも 1 回の前に取得されている場合にのみ機能します。

SYSRQ キーは、レジストリを編集して無効にすることができます。 レジストリ キー

```text
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\i8042prt\Parameters
```

という名前の値を作成する**BreakOnSysRq**、し、DWORD 0x0 と等しく設定します。 再起動します。 これが完了したら、ターゲット コンピューターのキーボードを SYSRQ キーを押すとはカーネル デバッガーを中断しません。

**Cdb KD をデバッグするとき。**

Cdb KD をデバッグする場合、ホスト デバッガー (CDB) によって CTRL + C がインターセプトされます。 使用する必要がありますにターゲット デバッガー (KD) を分割[ **CTRL + F** ](ctrl-f--break-to-kd-.md)代わりにします。

**注**  で WinDbg、CTRL キーを押しながら C キーは、[ショートカット キー](keyboard-shortcuts.md)ウィンドウからテキストをコピーに使用されます。 WinDbg で中断コマンドを実行するには、次のように使用します[CTRL + BREAK](debug---break.md)またはデバッグを選択します。 |。メニューから中断します。

 

 

 





