---
title: ドライバーの複数プロセッサ グループのサポートをテストするためのブート パラメーター
description: ドライバーの複数プロセッサ グループのサポートをテストするためのブート パラメーター
ms.assetid: 8ce311d6-a182-4d04-a453-81f6abe2043b
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: cc203d49ea8ca86362abb44aeeb8774b1f0c7762
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769584"
---
# <a name="boot-parameters-to-test-drivers-for-multiple-processor-group-support"></a>ドライバーの複数プロセッサ グループのサポートをテストするためのブート パラメーター


Windows 7 と Windows Server 2008 R2 では、64を超えるプロセッサを搭載したコンピューターがサポートされています。 このサポートは、[プロセッサグループ](https://docs.microsoft.com/windows/win32/procthread/processor-groups)を導入することによって可能になります。 テスト目的の場合は、グループのサイズを制限することで、複数の論理プロセッサを持つすべてのコンピューターに複数のプロセッサグループを構成できます。 これは、64以下の論理プロセッサを搭載したコンピューターで、複数のプロセッサグループの互換性をテストするためのドライバーとコンポーネントをテストできることを意味します。

**メモ**   Windows 7 で導入された*プロセッサグループ*の概念により、既存の Api と DDIs は、64を超える論理プロセッサを搭載したコンピューターで引き続き動作できます。 通常、グループのプロセッサは、64ビット長の affinity mask で表されます。 64個を超える論理プロセッサを搭載したコンピューターには、必ず1つ以上のグループが存在します。
プロセスが作成されると、そのプロセスは特定のグループに割り当てられます。 既定では、プロセスのスレッドは、同じグループのすべての論理プロセッサで実行できます。ただし、スレッドアフィニティは明示的に変更できます。 アフィニティマスクまたはプロセッサ番号を引数として受け取り、グループ番号ではない API または DDI への呼び出しは、呼び出し元スレッドのグループ内のそれらのプロセッサに対する影響または報告に限定されます。 これは、 **Getsysteminfo**などの関係マスクまたはプロセッサ番号を返す api または DDIs にも当てはまります。

Windows 7 以降では、アプリケーションまたはドライバーは、レガシ Api を拡張する関数を利用できます。 これらの新しいグループ対応関数は、グループ番号引数を使用してプロセッサ番号または関係マスクを明確に修飾するため、呼び出し元スレッドのグループの外部のプロセッサを操作できます。 コンピューター内の異なるグループで実行されているドライバーとコンポーネントの間の相互作用によって、レガシ Api または DDIs が関係している場合にバグが発生する可能性があります。 Windows 7 と Windows Server 2008 R2 では、グループに対応していない従来の Api を使用できます。 ただし、ドライバーの要件はより厳しくなります。 複数のプロセッサグループがあるコンピューターでのドライバーの機能の正確さを確認するには、プロセッサ数またはマスクを使用するすべての DDI を、プロセッサグループが付属していないパラメーターとして受け入れるか、プロセッサグループが付属していないプロセッサ番号またはマスクを返す必要があります。 複数のプロセスグループを持つコンピューターでは、これらの従来の非グループ対応 DDIs は、推定されるグループが、呼び出し元のスレッドが意図したものと異なる場合があるため、不規則に実行できます。 そのため、これらのレガシ DDIs を使用し、Windows Server 2008 R2 を対象とするドライバーは、新しい拡張バージョンのインターフェイスを使用するように更新する必要があります。 プロセッサの関係マスクまたはプロセッサ番号を使用する関数を呼び出さないドライバーは、プロセッサの数に関係なく、正常に動作します。 新しい DDIs を呼び出すドライバーは、以前のバージョンの Windows で実行できます。そのためには、WdmlibProcgrpInitialize ヘッダーを追加し、を呼び出し、[プロセッサグループ互換性ライブラリ](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)( [**WdmlibProcgrpInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/procgrp/nf-procgrp-wdmlibprocgrpinitialize)) に対してリンクします。

新しいグループ対応 Api と DDIs の詳細については、 [64 個を超える論理プロセッサを搭載したシステムをサポートするホワイトペーパー「開発者向けのガイドライン](https://download.microsoft.com/download/a/d/f/adf1347d-08dc-41a4-9084-623b1194d4b2/MoreThan64proc.docx)」をダウンロードしてください。

 

ドライバーおよびコンポーネントでプロセッサグループに関連する可能性のある問題を特定するには、 [**BCDEdit/set**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)オプションを使用します。 2つの BCD ブート構成設定**groupsize**と**maxgroup**を使用すると、複数の論理プロセッサを持つすべてのコンピューターを構成して、複数のプロセッサグループをサポートできます。 **Groupaware**オプションは、特定の DDIs の動作を変更し、テスト目的でグループ環境を操作します。

### <a name="span-idcreate_multiple_processor_groups_by_changing_the_group_sizespanspan-idcreate_multiple_processor_groups_by_changing_the_group_sizespancreate-multiple-processor-groups-by-changing-the-group-size"></a><span id="create_multiple_processor_groups_by_changing_the_group_size"></span><span id="CREATE_MULTIPLE_PROCESSOR_GROUPS_BY_CHANGING_THE_GROUP_SIZE"></span>グループサイズを変更して複数のプロセッサグループを作成する

**Groupsize**オプションは、グループ内の論理プロセッサの最大数を指定します。 既定では、 **groupsize**オプションは設定されておらず、64以下の論理プロセッサを搭載しているコンピューターにはグループ0のグループが1つあります。

**メモ**   物理プロセッサまたはプロセッサパッケージは、1つまたは複数のコア (プロセッサユニット) を持つことができ、それぞれに1つ以上の論理プロセッサを含めることができます。 オペレーティングシステムは論理プロセッサを1つの論理コンピューティングエンジンと見なします。

 

複数のプロセッサグループを作成するには、管理者特権でのコマンドプロンプトウィンドウで[**BCDEdit/set**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)を実行し、論理プロセッサの合計数よりも小さい**groupsize**の新しい*maxsize*値を指定します。 [グループサイズ] 設定はテスト用であるため、この設定で出荷システムを構成しないように注意してください。 *Maxsize*値は、1 ~ 64 の範囲の任意の累乗に設定できます。 このコマンドでは、次の構文を使用します。

```
bcdedit.exe /set groupsize maxsize
```

たとえば、次のコマンドは、グループ内のプロセッサの最大数を2に設定します。

```
bcdedit.exe /set groupsize 2
```

非 NUMA コンピューターに8つの論理プロセッサがある場合、 **groupsize**を2に設定すると、それぞれ2つの論理プロセッサを持つ4つのプロセッサグループが作成されます。

グループ 0: 1 2 つの論理プロセッサの1つのパッケージを含む NUMA ノード

グループ 1: 1 2 つの論理プロセッサの1つのパッケージを含む NUMA ノード

グループ 2: 1 2 つの論理プロセッサの1つのパッケージを含む NUMA ノード

グループ 3: 1 2 つの論理プロセッサの1つのパッケージを含む NUMA ノード

仕様として、非 NUMA コンピューターは1つの NUMA ノードを持つと見なされます。 NUMA ノードは複数のグループにまたがることができないため、コンピューターを再起動した後に、システムによって各グループのノードが作成されます。

**Groupsize**が物理プロセッサパッケージ (ソケット) の論理プロセッサの数よりも小さい値に設定されている場合、パッケージがグループに収まらないように、再起動時にパッケージの概念が再定義されます。 これは、実際に存在するよりも多くのパッケージがプロセッサトポロジ Api によって報告されることを意味します。 これは、 **groupsize**が設定されている場合に、Windows (パッケージレベル) プロセッサのライセンス制限によって一部のプロセッサパッケージが起動されない可能性があることも意味します。

プロセッサパッケージは、複数の NUMA ノードが定義されている場合、複数のグループにまたがることができ、システムはこれらのノードを別のグループに割り当てます。

サポートされるグループの数は、Windows によって制限されます。 この数値は、新しいバージョンの Windows または Service Pack のリリースで変更される可能性があります。 ドライバーまたはコンポーネントは、Windows が定数としてサポートするグループの数に依存しないようにする必要があります。 **Groupsize**ブートオプションに小さい値が使用されている場合、グループの数の制限によって、開始できる論理プロセッサの数が制限されることがあります。

テストに使用した**groupsize**設定を削除し、グループあたり64論理プロセッサの既定の設定に戻すには、次の BCDEdit コマンドを使用します。

```
bcdedit.exe /deletevalue groupsize
```

このコマンドは、 **groupsize**を64に設定した場合と同じです。

### <a name="span-idmaximize_the_number_of_processor_groupsspanspan-idmaximize_the_number_of_processor_groupsspanmaximize-the-number-of-processor-groups"></a><span id="maximize_the_number_of_processor_groups"></span><span id="MAXIMIZE_THE_NUMBER_OF_PROCESSOR_GROUPS"></span>プロセッサグループの数を最大にする

**Maxgroup**オプションは、複数の論理プロセッサと NUMA ノードを搭載したコンピューター上でプロセッサグループを作成する別の方法です。 **Maxgroup**ブートオプションは、NUMA 以外のコンピューターには影響しません。

グループの数を最大にするには、管理者特権でのコマンドプロンプトウィンドウで[**BCDEdit/set**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)コマンドを実行します。 このコマンドでは、次の構文を使用します。

```
bcdedit.exe /set maxgroup on
```

たとえば、2つの NUMA ノード、ノードごとに1つのプロセッサパッケージ、およびパッケージあたり4プロセッサコアを搭載したコンピューターで、合計8個の論理プロセッサを使用しているとします。

既定のグループ構成は次のとおりです。

グループ 0: 8 の論理プロセッサ、2つのパッケージ、2つの NUMA ノード

コマンドの後に「」と入力すると **、コマンドに**よって次のグループ構成が生成されます。

グループ 0: 4 の論理プロセッサ、1個のパッケージ、1つの NUMA ノード

グループ 1: 4 の論理プロセッサ、1個のパッケージ、1つの NUMA ノード

NUMA ノードは、グループの数を最大化するようにグループに割り当てられることに注意してください。

既定の設定に戻すには、次の**BCDEdit**コマンドを使用します。

```
bcdedit.exe /set maxgroup off
```

### <a name="span-idtest_multiple_group_compatibility_by_setting_the_group_aware_boot_optispanspan-idtest_multiple_group_compatibility_by_setting_the_group_aware_boot_optispantest-multiple-group-compatibility-by-setting-the-group-aware-boot-option"></a><span id="test_multiple_group_compatibility_by_setting_the_group_aware_boot_opti"></span><span id="TEST_MULTIPLE_GROUP_COMPATIBILITY_BY_SETTING_THE_GROUP_AWARE_BOOT_OPTI"></span>グループ対応ブートオプションを設定して、複数グループの互換性をテストする

Windows 7 と Windows Server 2008 R2 では、複数のプロセッサグループ環境内の複数のグループを対象とするドライバーとコンポーネントを強制する新しい BCD オプション (**groupaware**) が導入されました。 **Groupaware**オプションは、デバイスドライバーの一連の機能の動作を変更して、ドライバーやコンポーネントのクロスグループの非互換性を公開できるようにします。 コンピューターのアクティブな論理プロセッサが64以下の場合、 **groupsize**および**maxgroup**オプションと共に**groupaware**ブートオプションを使用して、複数のグループとドライバーの互換性をテストできます。

**Groupaware**ブートオプションを設定すると、オペレーティングシステムによって、プロセスがグループ0以外のグループで開始されるようになります。 これにより、ドライバーとコンポーネントの間でグループ間の相互作用が生じる可能性が高くなります。 また、このオプションは、グループ対応、 **Kesettargetprocessordpc**、 **KeSetSystemAffinityThreadEx**、および**KeRevertToUserAffinityThreadEx**ではないレガシ関数の動作も変更します。これにより、アクティブな論理プロセッサが含まれている最も番号の大きいグループが常に動作するようになります。 これらのレガシ関数のいずれかを呼び出すドライバーは、グループ対応の対応する関数 (**KeSetTargetProcessorDpcEx**、 **KeSetSystemGroupAffinityThread**、および**KeRevertToUserGroupAffinityThread**) を呼び出すように変更する必要があります。

互換性をテストするには、次の[**BCDEdit/set**](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--set)コマンドを使用します。

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
<th align="left">グループに対応していない従来の関数</th>
<th align="left">Windows 7 のグループ対応の置換</th>
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

 

コンピューターを既定の設定にリセットするには、次の**BCDEdit**コマンドを使用します。

```
bcdedit.exe /set groupaware off
```

 

 





