---
title: RunAs LowIL
description: TAEF では、低い整合性レベルのプロセス内でテストを実行します。
ms.assetid: 8FF26AB3-F473-4352-8951-D3F7DF366B5F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b920fcec53aa336f42e833ea175ed68cd9ab355
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569777"
---
# <a name="runas-lowil"></a>RunAs LowIL


TAEF では、低い整合性レベルのプロセス内でテストを実行します。

**注:**  

 

**注**  のバージョンの Windows Vista より前の Windows を実行するコンピューターでこのオプションはサポートされません。

 

## <a name="span-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspecifying-runas-on-the-command-line"></a><span id="Specifying_RunAs_on_the_Command_Line_"></span><span id="specifying_runas_on_the_command_line_"></span><span id="SPECIFYING_RUNAS_ON_THE_COMMAND_LINE_"></span>コマンドラインで RunAs を指定します。


``` syntax
te unittests\* /runas:lowil
```

## <a name="span-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanmarking-tests-with-runas"></a><span id="Marking_Tests_with_RunAs_"></span><span id="marking_tests_with_runas_"></span><span id="MARKING_TESTS_WITH_RUNAS_"></span>RunAs でテストをマークします。


テスト メタデータは、アセンブリ、クラスまたはテスト メソッドの実行の種類を指定できます。

**注**  メタデータで指定された RunAs 値、コマンドラインで指定された RunAs 値をオーバーライドします。 たとえば、テストが付いて**runas:system**テスト メタデータがあってもローカル システムとして実行されます **/runas:elevated**コマンドラインが指定されています。

 

例 (ネイティブ コード)

```ManagedCPlusPlus
class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(LowILTest)
        TEST_METHOD_PROPERTY(L"RunAs", L"LowIL")
    END_TEST_METHOD()
};
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[RunAs](runas.md)

 

 






