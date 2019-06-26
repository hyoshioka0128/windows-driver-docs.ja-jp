---
title: ドライバーの複数プロセッサ グループのサポートをテストするためのブート パラメーター
description: ドライバーの複数プロセッサ グループのサポートをテストするためのブート パラメーター
ms.assetid: 8ce311d6-a182-4d04-a453-81f6abe2043b
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2afd170e4fcd5cd644e9f7a2b877b14f6ee166a0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371637"
---
# <a name="boot-parameters-to-test-drivers-for-multiple-processor-group-support"></a>ドライバーの複数プロセッサ グループのサポートをテストするためのブート パラメーター


Windows 7 および Windows Server 2008 R2、64 を超えるプロセッサを搭載したコンピューターのサポートを提供します。 このサポートが導入することで可能になります[プロセッサ グループ](https://go.microsoft.com/fwlink/p/?linkid=155063)します。 テスト目的で、グループのサイズを制限することによって複数のプロセッサ グループに複数の論理プロセッサを搭載した任意のコンピューターを構成できます。 これは、ドライバーと 64 個以下の論理プロセッサを搭載したコンピューターで複数のプロセッサ グループの互換性のためのコンポーネントをテストすることを意味します。

**注**  の概念*プロセッサ グループ*Windows 7 で導入された、64 を超える論理プロセッサを搭載したコンピューターで作業を続行するには、既存の Api および Ddi できます。 通常、グループのプロセッサは、64 ビット長である、関係マスクで表されます。 64 を超える論理プロセッサを持つ任意のコンピューターは、1 つ以上のグループを必ずしもがあります。
プロセスが作成されたときに、プロセスが特定のグループに割り当てられます。 既定では、このプロセスのスレッドは、スレッドの関係を明示的に変更できますが、同じグループのすべての論理プロセッサで実行できます。 任意の API または取るアフィニティ マスクまたはプロセッサ番号を引数としてグループ数ではなく、DDI への呼び出しは、影響を与えたり、呼び出し元スレッドのグループにそれらのプロセッサでレポートに制限されます。 Api または Ddi のようなアフィニティ マスクまたはプロセッサ数を返すことの方も**GetSystemInfo**します。

Windows 7 以降、アプリケーション、ドライバーと、従来の Api を拡張する関数を使用します。 これらの新しいグループ対応関数は、プロセッサ数またはアフィニティ マスクを明確に修飾するために、グループの数値引数を受け取り、呼び出し元スレッドのグループの外部でプロセッサを操作できます。 ドライバーと、コンピューター内の各グループで実行されるコンポーネント間の相互作用には、従来の Api または Ddi が関係するバグが発生する可能性が導入されています。 Windows 7 および Windows Server 2008 R2 では、従来のグループに対応していない Api を使用できます。 ただし、ドライバーの要件より厳格なは。 1 つ以上のプロセッサ グループがあるコンピューター上のドライバーの機能の正確性は、プロセッサ数またはマスクを付属のプロセッサ グループのないパラメーターとして受け入れるか、プロセッサ数またはせずマスクを返します、DDI を置き換える必要があります、プロセッサ グループに付属します。 これらのレガシ グループ対応 Ddi は、推論されたグループのためのもので、どのような呼び出し元スレッドと異なる可能性があるために、複数のプロセス グループをされているコンピューターでが不安定になる実行できます。 したがって、ドライバーを使用して、これらのレガシ Ddi とが Windows Server 2008 R2 の対象には、インターフェイスの新しい拡張バージョンを使用して更新する必要があります。 呼び出さない任意の関数をドライバーを使用して、プロセッサ関係マスクまたはプロセッサ番号は、プロセッサの数に関係なく正しく動作します。 呼び出す新しい Ddi ドライバーは、procgrp.h ヘッダーを含めることで以前のバージョンの Windows で実行できる呼び出し[ **WdmlibProcgrpInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/procgrp/nf-procgrp-wdmlibprocgrpinitialize)、に対してリンク、[プロセッサ グループCompatibility Library](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index) (procgrp.lib)。

グループに対応の新しい Api と Ddi の詳細については、ホワイト ペーパーのダウンロード[64 を超える論理プロセッサを搭載したシステムのサポートします。開発者向けガイドライン](https://go.microsoft.com/fwlink/p/?linkid=147914)します。

 

潜在的なプロセッサ グループに関連する問題のドライバーとコンポーネントを識別するには、使用することができます、 [ **BCDEdit/set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)オプション。 2 つの BCD ブートの構成設定、**サイズ**と**maxgroup**、複数のプロセッサ グループをサポートするために複数の論理プロセッサを搭載した任意のコンピューターを構成することができます。 **Groupaware**オプション Ddi 特定の動作を変更し、テスト目的でグループ環境を操作します。

### <a name="span-idcreatemultipleprocessorgroupsbychangingthegroupsizespanspan-idcreatemultipleprocessorgroupsbychangingthegroupsizespancreate-multiple-processor-groups-by-changing-the-group-size"></a><span id="create_multiple_processor_groups_by_changing_the_group_size"></span><span id="CREATE_MULTIPLE_PROCESSOR_GROUPS_BY_CHANGING_THE_GROUP_SIZE"></span>グループのサイズを変更することで複数のプロセッサ グループを作成します。

**サイズ**オプションは、グループ内の論理プロセッサの最大数を指定します。 既定で、**サイズ**オプションが設定されていないと、任意のコンピューターで 64 個以下の論理プロセッサが 1 つのグループ、グループ 0 です。

**注**  物理プロセッサまたはプロセッサ パッケージは、1 つ以上のコアまたはプロセッサ ユニット、それぞれが 1 つまたは複数の論理プロセッサを含めることができますを持つことができます。 オペレーティング システムでは、1 つの論理コンピューティング エンジンとして、論理プロセッサと見なします。

 

複数のプロセッサ グループを作成するには、実行[ **BCDEdit/set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)で管理者特権のコマンド プロンプト ウィンドウと、新しい指定*maxsize*値**サイズ**論理プロセッサの合計数より小さいされています。 グループ サイズの設定はテストをこの設定で配布システムを構成する必要がありますに注意してください。 *Maxsize*値は 1 ~ 64 の範囲での 2 の累乗に設定することができます。 コマンドは、次の構文を使用します。

```
bcdedit.exe /set groupsize maxsize
```

たとえば、次のコマンドは、2 グループのプロセッサの最大数を設定します。

```
bcdedit.exe /set groupsize 2
```

非 NUMA コンピューターに 8 個の論理プロセッサがある場合は、設定、**サイズ**2 に 2 つの論理プロセッサを持つ 4 つのプロセッサ グループを作成します。

グループ 0:2 つの論理プロセッサの 1 のパッケージを含む 1 つの NUMA ノード

グループ 1:2 つの論理プロセッサの 1 のパッケージを含む 1 つの NUMA ノード

グループ 2:2 つの論理プロセッサの 1 のパッケージを含む 1 つの NUMA ノード

グループ 3:2 つの論理プロセッサの 1 のパッケージを含む 1 つの NUMA ノード

仕様では、非 NUMA コンピューターが 1 つの NUMA ノードがあると見なされます。 NUMA ノードには、グループをまたがることはできません、ため、コンピューターの再起動後、システム グループごとにノードを作成します。

場合**サイズ**の概念と、パッケージの再起動、パッケージがグループにまたがらないようにシステムの再定義 (ソケット) の物理プロセッサ パッケージの論理プロセッサ数よりも小さい値に設定されます。 これは、実際に含まれるその他のパッケージがプロセッサ トポロジ Api によって報告されることを意味します。 ライセンスの制限 (パッケージ レベル) の Windows プロセッサが、プロセッサ パッケージによってをいつ起動を妨げる可能性ことも意味**サイズ**設定されます。

複数の NUMA ノード内に定義され、システムでは、さまざまなグループにこれらのノードが割り当てられます、プロセッサ パッケージはグループにまたがることができます。

Windows では、サポートされているグループの数を制限します。 この数は、Windows の場合、またはサービス パックのリリースでの新しいバージョンで変更でした。 ドライバーまたはコンポーネントは、定数としてサポートしている Windows グループの数に依存する必要があります。 グループの数に制限は、小さい値が使用されるときに開始する許可されている論理プロセッサの数を制限ことができます、**サイズ**ブート オプション。

削除する、**サイズ**次の BCDEdit コマンドを使用するをテストするために使用されると、戻り値を 64 の論理プロセッサ グループごとの既定の設定に設定します。

```
bcdedit.exe /deletevalue groupsize
```

このコマンドは、のと同じ**サイズ**64 です。

### <a name="span-idmaximizethenumberofprocessorgroupsspanspan-idmaximizethenumberofprocessorgroupsspanmaximize-the-number-of-processor-groups"></a><span id="maximize_the_number_of_processor_groups"></span><span id="MAXIMIZE_THE_NUMBER_OF_PROCESSOR_GROUPS"></span>プロセッサ グループ数を最大化します。

**Maxgroup**オプションは、複数の論理プロセッサと NUMA ノードを使用しているコンピューターのプロセッサ グループを作成することもできます。 **Maxgroup**ブート オプションが非 NUMA コンピューターに影響を与えません。

グループの数を最大化するには、実行、 [ **BCDEdit/set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)管理者特権のコマンド プロンプト ウィンドウでコマンド。 コマンドは、次の構文を使用します。

```
bcdedit.exe /set maxgroup on
```

たとえば、2 つの NUMA ノード、ノードごとに 1 個のプロセッサ パッケージとパッケージ、合計で 8 個の論理プロセッサごとの 4 つのプロセッサ コアを持つコンピューターがあるとします。

既定のグループの構成は次のとおりです。

グループ 0:8 個の論理プロセッサ、2 つのパッケージ、2 つの NUMA ノード

入力した場合、 **bcdedt.exe maxgroup を設定/** コマンドのコマンドは、再起動後に、次のグループの構成を生成します。

グループ 0:4 つの論理プロセッサ、1 個のパッケージ、1 つの NUMA ノード

グループ 1:4 つの論理プロセッサ、1 個のパッケージ、1 つの NUMA ノード

NUMA ノードがグループの数を最大化する方法でグループに割り当てられていることに注意してください。

既定の設定を変更する、次を使用して、 **BCDEdit**コマンド。

```
bcdedit.exe /set maxgroup off
```

### <a name="span-idtestmultiplegroupcompatibilitybysettingthegroupawarebootoptispanspan-idtestmultiplegroupcompatibilitybysettingthegroupawarebootoptispantest-multiple-group-compatibility-by-setting-the-group-aware-boot-option"></a><span id="test_multiple_group_compatibility_by_setting_the_group_aware_boot_opti"></span><span id="TEST_MULTIPLE_GROUP_COMPATIBILITY_BY_SETTING_THE_GROUP_AWARE_BOOT_OPTI"></span>グループの対応のブート オプションを設定して複数のグループの互換性をテストします。

Windows 7 および Windows Server 2008 R2 には、新しい BCD オプションを導入しました (**groupaware**) を強制的にドライバーとコンポーネントを複数のプロセッサ グループ環境で複数のグループに注意してください。 **Groupaware**オプションは、一連のドライバーとコンポーネントのグループ間の非互換性を公開するデバイス ドライバーの関数の動作を変更します。 使用することができます、 **groupaware**ブート オプションと共に、**サイズ**と**maxgroup**をコンピューターに 64 が設定されている場合、複数のグループとドライバーの互換性をテストするためのオプションまたはアクティブな論理プロセッサの数。

ときに、 **groupaware**ブート オプションが設定されている、オペレーティング システムによりグループ 0 以外のプロセスが開始されているようになります。 これにより、ドライバーとコンポーネント間のグループ間の相互作用の機会が増えます。 オプションでは、グループに対応していない従来の関数の動作も変更されます**KeSetTargetProcessorDpc**、 **KeSetSystemAffinityThreadEx**、および**KeRevertToUserAffinityThreadEx**常にアクティブな論理プロセッサを含む最上位の番号付きグループで動作するようにします。 呼び出すグループ対応、対応する従来これらの関数のいずれかを呼び出すドライバーを変更する必要があります (**KeSetTargetProcessorDpcEx**、 **KeSetSystemGroupAffinityThread**、および**KeRevertToUserGroupAffinityThread**)、

次を使用して互換性をテストする[ **BCDEdit/set** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)コマンド。

```
bcdedit.exe /set groupaware on
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">レガシ グループ以外に注意してください関数</th>
<th align="left">Windows 7 対応のグループの置換</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KeSetTargetProcessorDpc</p></td>
<td align="left"><p>KeSetTargetProcessorDpcEx</p></td>
</tr>
<tr class="even">
<td align="left"><p>KeSetSystemAffinityThreadEx</p></td>
<td align="left"><p>KeSetSystemGroupAffinityThread</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KeRevertToUserAffinityThreadEx</p></td>
<td align="left"><p>KeRevertToUserGroupAffinityThread</p></td>
</tr>
</tbody>
</table>

 

次を使用して、コンピューターを既定の設定をリセットする**BCDEdit**コマンド。

```
bcdedit.exe /set groupaware off
```

 

 





