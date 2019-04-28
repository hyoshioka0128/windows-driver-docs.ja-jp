---
title: RunAs Restricted
description: TAEF 確実にテストが制限付きのプロセスで実行されます。
ms.assetid: 1565344E-2CF9-4E08-9BA2-23FE1D677ABA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 046f3937f203a9b8d18114e8cc62eedcdafa9f0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361692"
---
# <a name="runas-restricted"></a>RunAs Restricted


TAEF 確実にテストが制限付きのプロセスで実行されます。

**注**  のバージョンの Windows Vista より前の Windows を実行するコンピューターでは、管理者プロセスから制限のテストを実行する必要があります。

 

## <a name="span-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspecifying-runas-on-the-command-line"></a><span id="Specifying_RunAs_on_the_Command_Line_"></span><span id="specifying_runas_on_the_command_line_"></span><span id="SPECIFYING_RUNAS_ON_THE_COMMAND_LINE_"></span>コマンドラインで RunAs を指定します。


``` syntax
te unittests\* /runas:restricted
```

## <a name="span-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanmarking-tests-with-runas"></a><span id="Marking_Tests_with_RunAs_"></span><span id="marking_tests_with_runas_"></span><span id="MARKING_TESTS_WITH_RUNAS_"></span>RunAs でテストをマークします。


テスト メタデータは、アセンブリ、クラスまたはテスト メソッドの実行の種類を指定できます。

**注**  メタデータで指定された RunAs 値、コマンドラインで指定された RunAs 値をオーバーライドします。 たとえば、テストが付いて**runas:system**テスト メタデータがあってもローカル システムとして実行されます **/runas:elevated**コマンドラインが指定されています。

 

例 (ネイティブ コード)

```ManagedCPlusPlus
class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(RestrictedTest)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
    END_TEST_METHOD()
};
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[RunAs](runas.md)

 

 






