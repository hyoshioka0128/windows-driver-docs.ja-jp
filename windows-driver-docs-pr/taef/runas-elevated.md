---
title: RunAs の管理者特権
description: TAEF が確実に必要な場合は、テストを実行する管理者特権でのプロセスによって昇格されたプロセスでテストを実行します。
ms.assetid: 6292E431-6EB5-4962-BBB0-B86FC4CE4643
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b31b4353a29f00362cadf84322440197bd11e94d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529378"
---
# <a name="runas-elevated"></a>RunAs の管理者特権


TAEF が確実に必要な場合は、テストを実行する管理者特権でのプロセスによって昇格されたプロセスでテストを実行します。

**注:RunAs でマークされたテストを実行するには、administrators グループのメンバーである TAEF を実行するユーザー管理者特権でを = です。** これは、非管理者に昇格分割トークンがあるないという事実を原因。 RunAs でマークされているテストを実行しようとしている管理者以外の場合は、管理者特権を =**ブロックされているために、テストをマークは**します。

**注**  のバージョンの Windows Vista より前の Windows を実行するコンピューターでは、管理者プロセスから管理者特権でのテストを実行する必要があります。

 

## <a name="span-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspecifying-runas-on-the-command-line"></a><span id="Specifying_RunAs_on_the_Command_Line_"></span><span id="specifying_runas_on_the_command_line_"></span><span id="SPECIFYING_RUNAS_ON_THE_COMMAND_LINE_"></span>コマンドラインで RunAs を指定します。


``` syntax
te unittests\* /runas:elevated
```

## <a name="span-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanmarking-tests-with-runas"></a><span id="Marking_Tests_with_RunAs_"></span><span id="marking_tests_with_runas_"></span><span id="MARKING_TESTS_WITH_RUNAS_"></span>RunAs でテストをマークします。


テスト メタデータは、アセンブリ、クラスまたはテスト メソッドの実行の種類を指定できます。

**注**  メタデータで指定された RunAs 値、コマンドラインで指定された RunAs 値をオーバーライドします。 たとえば、テストが付いて**runas:system**テスト メタデータがあってもローカル システムとして実行されます **/runas:elevated**コマンドラインが指定されています。

 

例 (ネイティブ コード)

```ManagedCPlusPlus
class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(ElevatedTest)
        TEST_METHOD_PROPERTY(L"RunAs", L"Elevated")
    END_TEST_METHOD()
};
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[RunAs](runas.md)

 

 






