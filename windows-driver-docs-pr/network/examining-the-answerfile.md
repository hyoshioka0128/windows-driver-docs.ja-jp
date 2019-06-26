---
title: AnswerFile の調査
description: AnswerFile の調査
ms.assetid: 42d58786-e50c-43c2-b673-5f23c9930ee7
keywords:
- テスト ネットワーク コンポーネントをアップグレード WDK
- 応答ファイルの WDK ネットワーク
- アップグレードのテストの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac0bbe0a55bbafef589e1264894e1c6033f69a2f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363430"
---
# <a name="examining-the-answerfile"></a>AnswerFile の調査





**注**  Microsoft Windows XP では、ベンダーから提供されたネットワークのアップグレードはサポートされていない (SP1 以降)、Microsoft Windows Server 2003、および以降のオペレーティング システム。

 

アップグレード対象のシステム「セットアップは、コピー ファイル」の進行状況バーが表示される、前にすぐに、応答ファイルが作成されます。 NetSetup とベンダーから提供されたネットワークの移行、Dll は、応答ファイルでセクションを作成し、フェーズのアップグレード、Winnt32 中にこれらのセクションにエントリを書き込みます。

応答ファイルを確認するには c: をコピーして\\$win\_nt$。 ~ bt\\winnt.sif %temp% にします。 クリックすることができます、応答ファイルがコピーされると、**キャンセル**ファイルのコピーをキャンセルします。 ファイルのコピーが完了するまで待機する必要はありません。

次の表では、応答ファイルと、対応するエントリの各セクションを含むネットワーク コンポーネントに関連する最上位レベルのセクションを示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">セクション</th>
<th align="left">エントリが含まれています。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>NetAdapters</strong></p></td>
<td align="left"><p>ISDN アダプターを含む、ネットワーク アダプター</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>AsyncAdapters</strong></p></td>
<td align="left"><p>非同期アダプター</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NetProtocols</strong></p></td>
<td align="left"><p>ネットワーク プロトコル</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NetServices</strong></p></td>
<td align="left"><p>ネットワーク サービス</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>NetClients</strong></p></td>
<td align="left"><p>ネットワーク クライアント</p></td>
</tr>
</tbody>
</table>

 

**注**  **NetClient**コンポーネントは Windows 8.1、Windows Server 2012 R2 で非推奨以降。

 

Winnt32 フェーズ中に検出された各ネットワーク コンポーネント、NetSetup は、応答ファイルの適切な最上位レベルのセクションにエントリを書き込みます。 各エントリには、次の形式があります。

params します。*postupgrade ID*

*Postupgrade ID*エントリが Windows 2000 またはそれ以降のデバイス ID NetSetup がコンポーネントの netmap.inf ファイルのファイルから取得します。

各エントリは、応答ファイルで、そのコンポーネントの parameters セクションの名前を指定します。 たとえば、コンポーネントの Windows 2000 またはそれ以降のデバイス ID が netadapter2、対応するエントリの場合、 **NetAdapters**セクションは**params.netadapter2**します。 最上位レベルのセクションでは、および応答ファイルでパラメーター セクションでは、DLL のネットワークの移行には表示されません。

NetSetup コンポーネントのパラメーター セクション名に拡張子が追加**OemSection**を作成する、 *OEM セクション*コンポーネントの名前。 たとえば、パラメーターのセクションの場合に、コンポーネントは params.netadapter2、 *OEM セクション*コンポーネントが params.netadapter2.OemSection の名前します。 NetSetup 渡します、 *OEM セクション*名、 *szSectionName*パラメーターを[ **DoPreUpgradeProcessing** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545634(v=vs.85))によって提供される関数コンポーネントのネットワーク移行 DLL。 **DoPreUpgradeProcessing**関数呼び出し、 [ **NetUpgradeAddSection** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559063(v=vs.85))関数を作成する、 *OEM セクション*コンポーネントで、応答ファイル。 **DoPreUpgradeProcessing**関数から呼び出し、 [ **NetUpgradeAddLineToSection** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559059(v=vs.85))をコンポーネントに固有の情報を追加する、 *OEM セクション*.

応答ファイルの次の部分とを示していますのセクションでは、ネットワーク アダプターのエントリが Windows 2000 またはそれ以降のデバイス ID が**adapter2**:

```INF
[NetAdapter]              ;top-level adapters section
adapter2=params.adapter2      ;entry for adapter2
[params.adapter2]          ;parameters section for adapter2
InfID=adapter2            ;Windows 2000 or later device ID
OemSection=params.adapter2.OemSection  ;Identifies the OemSection

[params.adapter2.OemSection]  ;OemSection created by migration DLL
InfToRunAfterInstall="", adapter2.SectionToRun ;Written by DLL

[adapter2.SectionToRun]      ;Section created by migration DLL
AddReg=adapter2.SectionToRun.AddReg ;AddReg directive

[adapter2.SectionToRun.AddReg] ;AddReg section created by DLL
HKR,0\0,IsdnPhoneNumber,0,"111-1111" ;AddReg entries written by DLL
HKR,0\1,IsdnPhoneNumber,0,"222-2222"
HKR,0\0,IsdnSpid,0,"111"
HKR,0\1,IsdnSpid,0,"222"
HKR,0,IsdnSwitchType,0x00010001,1
```

NetSetup を GUI モード フェーズでは、検出、 [ **InfToRunAfterInstall** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559059(v=vs.85))移行 DLL によって書き込まれたキーを**params.adapter2.OemSection**の例では、応答ファイル。 このキーでの指示に従って NetSetup の処理、 **adapter2 します。SectionToRun.AddReg**セクション。 **Adapter2 します。SectionToRun.AddReg**セクションが NetSetup パラメーター値を Windows 2000 またはそれ以降のレジストリで adapater2 のインスタンス キーに追加するように指示します。 これらのパラメーター値は、DLL が adapter2 から読み取り、移行が、アップグレードの Winnt32 フェーズ中にレジストリのアップグレード前のパラメーター値と一致する必要があります。

ネットワーク移行 DLL は、GUI モード フェーズでは、読み込まれる場合、 [ **DoPreUpgradeProcessing** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545634(v=vs.85))関数の設定、NUA\_ロード\_POST\_アップグレード フラグ。 このフラグによって、書き込む NetSetup、 **OemDllToLoad**応答ファイルで、コンポーネントのパラメーター セクションに入力します。 **OemDllToLoad**エントリと NetSetup GUI モード フェーズ中に、コンポーネントの移行 DLL を読み込めません。

次の例は、応答ファイルのセクションでは、コンポーネントのエントリがネットワーク移行 GUI モード フェーズ中に DLL が読み込まれます。

```INF
[NetAdapter]              ;top-level adapters section
adapter2=params.adapter2      ;entry for adapter2
[params.adapter2]          ;parameters section for adapter2
InfID=adapter2            ;postupgrade device ID
OemSection=params.adapter2.OemSection;Identifies the OemSection
OemDllToLoad=c:\temp\oem0001\migration.dll
```

注、 **OemDllToLoad**内のエントリ、 **params.adapter2**セクション。 また、移行 DLL が作成されないことに注意してください、 **params.adapter2.OemSection**します。 移行の DLL は、GUI モード フェーズ中に読み込まれますが、通常は書き込まれません、 **InfToRunAfterInstall**応答ファイルにキー。 DLL は、インストール後、アップグレードを実行します。そのため、その作成する必要はありません、 *Oem セクション*NetSetup GUI モードのフェーズ中に実行するためのディレクティブを含む名前。

 

 





