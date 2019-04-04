---
title: Pvk2Pfx
description: Pvk2Pfx (Pvk2Pfx.exe) は、コマンド ライン ツールのコピーの公開キーと秘密キーの Personal Information Exchange (.pfx) ファイルに .spc、.cer、.pvk ファイルに含まれている情報。
ms.assetid: f3fb3703-0e33-4d7f-b2ad-52bc035e01de
keywords:
- Pvk2Pfx ドライバーの開発ツール
topic_type:
- apiref
api_name:
- Pvk2Pfx
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e0a35557cca9be560c18d8b359b88a585edd4d6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582275"
---
# <a name="pvk2pfx"></a>Pvk2Pfx


Pvk2Pfx (Pvk2Pfx.exe) は、コマンド ライン ツールのコピーの公開キーと秘密キーの Personal Information Exchange (.pfx) ファイルに .spc、.cer、.pvk ファイルに含まれている情報。

```
    pvk2pfx /pvk 
    pvkfilename.pvk [/pi pvkpassword] /spc spcfilename.ext [/pfx pfxfilename.pfx [/po pfxpassword] [/f]]
```

### <a name="span-idswitchesandargumentsspanspan-idswitchesandargumentsspanswitches-and-arguments"></a><span id="switches_and_arguments"></span><span id="SWITCHES_AND_ARGUMENTS"></span>スイッチと引数

<span id="_PVK_PVKFILENAME.PVK"></span>**/pvk** *pvkfilename.pvk*  
.Pvk ファイルの名前を指定します。

<span id="_SPC_SPCFILENAME.EXT"></span>**/spc** *spcfilename.ext*  
拡張機能と名前を指定します、[ソフトウェア発行元証明書 (SPC)](https://msdn.microsoft.com/library/windows/hardware/ff552299)証明書を含むファイル。 ファイルは、.spc ファイルまたは .cer ファイルのいずれかにすることはできます。

<span id="_PFX_PFXFILENAME.PFX"></span>**/pfx** *pfxfilename.pfx*  
.Pfx ファイルの名前を指定します。

<span id="_pi_pvkpassword"></span><span id="_PI_PVKPASSWORD"></span>**/pi** *pvkpassword*  
.Pvk ファイルのパスワードを指定します。

<span id="_po_pfxpassword"></span><span id="_PO_PFXPASSWORD"></span>**/po** *pfxpassword*  
.Pfx ファイルのパスワードを指定します。 .Pfx ファイルのパスワードが指定されていない場合、.pfx ファイルのパスワードは .pvk ファイルのパスワードと同じになります。

<span id="_f"></span><span id="_F"></span>**/f**  
指定したのと同じ名前を持つ 1 つが存在する場合は、.pfx ファイルを上書きする Pvk2Pfx を構成します、 **- pfx**スイッチします。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

場合、 **- pfx** *pfxfilename.pfx*スイッチが指定されていない、pvk2pfx 無視、 **po** *パスワード*スイッチと **-f**スイッチ、およびその対応するパスワードと .pfx ファイルの名前のユーザーに求めるウィザードが表示されます。

使用するには、 [ **SignTool** ](signtool.md)に準拠している方法で、SPC を使用してドライバーに署名するためのツール、[カーネル モード コードの署名ポリシー](https://msdn.microsoft.com/library/windows/hardware/ff548231)、SPC 情報に追加する必要がありますドライバーに署名するローカル コンピューターの個人証明書ストア。 SPC 情報を個人証明書ストアに追加する方法については、[ソフトウェア発行元証明書](https://msdn.microsoft.com/library/windows/hardware/ff552299)を参照してください。

Pvk2Pfx ツールの 32 ビット バージョンが、箱にある\\x86 WDK のフォルダー。 ツールの 64 ビット バージョンが、箱にある\\WDK の x64。 たとえば、Windows 10 を実行している x64 ベースのコンピューター、パスは、c:\\Program Files (x86)\\Windows キット\\10\\bin\\x64。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

次のコマンドでは、Mypvkfile.pvk および Myspcfile.spc から Mypfxfile.pfx .pfx ファイルを生成します。 コマンドには、.pfx ファイル Mypfxfile.pfx のパスワードとなる .pvk ファイルのパスワード mypassword が用意されています。 Mypfxfile.pfx、という名前の既存のファイルがある場合、 **-f**スイッチに、既存のファイルを新しいファイルに置き換える Pvk2Pfx ツールを構成します。

```
pvk2pfx -pvk mypvkfile.pvk -pi mypassword -spc myspcfile.spc -pfx mypfxfile.pfx -f
```

 

 





