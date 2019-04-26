---
title: GPIO コント ローラーのデバイス固有のメソッド (_DSM)
description: Microsoft、さまざまなデバイス固有クラス通信は Windows では、汎用の I/O (GPIO) ドライバー スタックとプラットフォームのファームウェアをサポートするには、特定のデバイス メソッド (_DSM)、ACPI に GPIO コント ローラーの下に含めることができるを定義します名前空間。
ms.assetid: 2891A78C-8C4F-4FE4-AB69-402F04DFA885
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9223bb68b3869bafa9e3c04a3c41c6781f42534
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337618"
---
# <a name="gpio-controller-device-specific-method-dsm"></a>デバイス固有のメソッドに GPIO コント ローラー (\_DSM)


Microsoft をさまざまなデバイス固有クラス通信は Windows では、汎用の I/O (GPIO) ドライバー スタックとプラットフォームのファームウェアをサポートするには、デバイス固有のメソッドを定義します (\_DSM) を GPIO コント ローラーの下に含めることができます。ACPI 名前空間。

現時点では、このメソッドは、2 つの関数を定義します。

-   **関数のインデックス 0**:標準のクエリ機能をすべて\_DSM メソッドを提供する必要は。
-   **関数インデックス 1**:コント ローラーのない ActiveBoth ピンの GPIO スタックに通知 ActiveBoth 極性関数は、低ロジックをアサートします。 GPIO スタックでは、こと ActiveBoth ピンがアサートされるロジック、低いため、この機能により、その既定値を特定のピンをオーバーライドするプラットフォームを前提としています。

## <a name="guid-definition"></a>GUID の定義


GPIO コント ローラーの GUID \_DSM メソッドとして定義されています。

`{4F248F40-D5E2-499F-834C-27758EA1CD3F}`

## <a name="function-0"></a>関数 0


関数 0 の各\_DSM がサポートされている関数のインデックスのセットを返しますは常に必要とするクエリ関数を示します。 関数 0 の定義、9.14.1、セクションを参照してください。"\_DSM (デバイスの特定のメソッド)"で、 [ACPI 5.0 仕様](https://www.uefi.org/specifications)します。

## <a name="function-1"></a>関数 1


GPIO コント ローラーの関数の 1 のパラメーター \_DSM メソッドは次のように定義されます。

### <a name="arguments"></a>引数

-   **Arg0:** GPIO コント ローラーの UUID \_DSM

    `// GUID: {4F248F40-D5E2-499F-834C-27758EA1CD3F}`

    `DEFINE_GUID (GPIO_CONTROLLER _DSM_GUID,`

    `0x4f248f40, 0xd5e2, 0x499f, 0x83, 0x4c, 0x27, 0x75, 0x8e, 0xa1, 0xcd. 0x3f);`

-   **Arg1:** リビジョン ID

    `#define GPIO_CONTROLLER _DSM_REVISION_ID     0`

-   **Arg2:** ActiveBoth の関数のインデックスは、極性をアサートします。

    `#define GPIO_CONTROLLER_DSM_ACTIVE_BOTH_POLARITY_FUNCTION_INDEX  1`

-   **Arg3:** パッケージを空 (未使用)

### <a name="return"></a>戻り値

GPIO コント ローラーで、pin のコント ローラーの相対 pin 番号は、それぞれが、整数のパッケージ:

-   ActiveBoth 割り込みのように定義し、
-   アサートされている状態では*いない*低ロジック (つまり、*は*ロジック高)。

たとえば、エミュレートの ActiveBoth pin がプッシュ ボタンのデバイスに接続している場合、pin を入力、*アサート*状態 (pin の入力のレベル ロジック高)、ユーザーが、ボタンを押すし、ユーザーが保持している間に、アサートされた状態にとどまります、ボタンを押したままです。 ユーザーがボタンを離すと、暗証番号 (pin) の状態が*unasserted* (ロジック-低の入力レベル)。

## <a name="asl-code-example"></a>ASL コードの例


ASL の次のコード例では、ActiveHigh の初期の極性が GPIO ピンのセットを識別します。

```asl
//
// _DSM - Device-Specific Method
//
// Arg0:    UUID       Unique function identifier
// Arg1:    Integer    Revision Level
// Arg2:    Integer    Function Index (0 = Return Supported Functions)
// Arg3:    Package    Parameters
//

Function(_DSM,{BuffObj, PkgObj, IntObj},{BuffObj, IntObj, IntObj, PkgObj})
{

    //
    // Switch based on which unique function identifier was passed in
    //

    //
    // GPIO CLX UUID
    //

    If(LEqual(Arg0,ToUUID("4F248F40-D5E2-499F-834C-27758EA1CD3F")))
    {
        switch(Arg2)
        {

            //
            // Function 0: Return supported functions, based on 
            //    revision
            //

            case(0)
            {
                // Revision 0+: Functions 0 & 1 are supported
                return (Buffer() {0x3})
            }

            //
            // Function 1: For emulated ActiveBoth controllers, 
            //    returns a package of controller-relative pin
            //    numbers. Each corresponding pin will have an
            //    initial polarity of ActiveHigh.
            //
            //    A pin number of 0xffff is ignored.
            //

            case(1)
            {     
                // Marks pins 0x28, 0x29 and 0x44 to be ActiveHigh.
                Return (Package() {0x28, 0x29, 0x44})
            }

            //
            // Unrecognized function for this revision
            //

            default
            {
                BreakPoint
            }
        }
    }
    else
    {
        //
        // If this is not one of the UUIDs we recognize, then return
        // a buffer with bit 0 set to 0 to indicate that no functions
        // are supported for this UUID.
        //

        return (Buffer() {0})
    }
}
```

 

 




