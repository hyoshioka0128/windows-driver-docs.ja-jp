---
title: RunAs System
description: TAEF は、ローカル システムとして、テストを実行します。
ms.assetid: E1138F36-D043-458A-8424-C649854CB7EE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c4e4828404dfe8cb55c8461cc89e567ed7cfa0e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326007"
---
# <a name="runas-system"></a>RunAs System


TAEF は、ローカル システムとして、テストを実行します。

**注**  任意のユーザー インターフェイス (UI) を作成しないでくださいローカル システムとして実行することをテストします。 使用してテストから、デスクトップ上で起動される実行可能ファイルに、UI 関連のコードを移動する必要がある場合は、テストは、作成、UI と対話したりする必要が[ **CreateProcessAsUser 関数**](https://msdn.microsoft.com/library/windows/desktop/ms682429)します。

 

## <a name="span-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspan-idspecifyingrunasonthecommandlinespanspecifying-runas-on-the-command-line"></a><span id="Specifying_RunAs_on_the_Command_Line_"></span><span id="specifying_runas_on_the_command_line_"></span><span id="SPECIFYING_RUNAS_ON_THE_COMMAND_LINE_"></span>コマンドラインで RunAs を指定します。


``` syntax
te unittests\* /runas:system
```

## <a name="span-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanspan-idmarkingtestswithrunasspanmarking-tests-with-runas"></a><span id="Marking_Tests_with_RunAs_"></span><span id="marking_tests_with_runas_"></span><span id="MARKING_TESTS_WITH_RUNAS_"></span>RunAs でテストをマークします。


テスト メタデータは、アセンブリ、クラスまたはテスト メソッドの実行の種類を指定できます。

**注**  メタデータで指定された RunAs 値、コマンドラインで指定された RunAs 値をオーバーライドします。 たとえば、テストが付いて**runas:system**テスト メタデータがあってもローカル システムとして実行されます **/runas:elevated**コマンドラインが指定されています。

 

例 (ネイティブ コード)

```ManagedCPlusPlus
class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(SystemTest)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()
};
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[RunAs](runas.md)

 

 






