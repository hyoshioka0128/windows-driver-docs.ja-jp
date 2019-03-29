---
title: プロパティ シートを作成します。
description: プロパティ シートを作成します。
ms.assetid: 04fa34fd-86d6-4017-a6da-9882d65674e3
keywords:
- プロパティ シートの WDK DirectInput、作成します。
- ゲーム コント ローラー WDK DirectInput、プロパティ シートの作成
- コントロール パネルの WDK DirectInput、プロパティ シートの作成
- プロパティ シート アプリケーション WDK DirectInput をサンプルします。
- カスタム プロパティ シートの WDK DirectInput
- WDK DirectInput テンプレート
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4e1204fcafa9c1bc61f0a41ca6ee26c7c26661d9
ms.sourcegitcommit: c4dc4a78ea33537bd47fc7fb666cfd0718d302e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2019
ms.locfileid: "58349261"
---
# <a name="creating-your-property-sheet"></a>プロパティ シートを作成します。

この例では、DirectInput の多くの側面について説明し、独自のカスタム プロパティ シートの適切な開始点を提供します。

## <a name="create-your-own-property-sheet"></a>プロパティ シートを作成します。

ゼロからカスタムのプロパティ シートの作成は、比較的単純なプロセスです。

1. プロパティ ページを識別する GUID を作成します。

   * プロパティ ページ (1 つのみ、ページ数に関係なく) の GUID を作成する (これは、Microsoft Windows SDK に含まれています) GuidGen ツールを使用します。 アプリケーション固有のインクルード ファイルでは、これを定義します。
   * 必須の DllGetClassObject および DllCanUnloadNow を作成します。
   * Dicpl.h で定義されている COM ClassFactory の実装を作成します。
   * 実装を作成、 **IDIGamgeCntrlPropSheet**インターフェイス。
   * マイ コンピューターに定義された GUID を追加、Regedit を使用して\\HKEY\_クラス\_ルート\\CLSID キー。 次に、キー InProcHandler32 と InProcServer32 キーを追加します。
   * プロパティ シート DLL の場所を指す InProcServer32 エントリの (既定値) のエントリを変更します。 例は次のようになります。"C:\\マイ\_デバイス\\マイ\_propertysheet.dll"。 この例では、ProgID のエントリを使用します。 これは必要はありませんが、多くの場合、その GUID に存在するモジュールに関する情報の格納に使用します。

2. 任意の Windows アプリケーションの場合と同様に、ダイアログ テンプレートとダイアログ プロシージャを作成します。

    > [!NOTE]
    > 独立したダイアログ ボックスとして、ページを起動するウィンドウとしてのプロパティ シートのテスト コンテナーを記述することがあります。 この時点では、DirectInput のコントロール パネル にする必要があります、既存のコントロール パネルを変換することも可能性があります。

3. 設定、 [ **DIGCPAGEINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff538484)と[ **DIGCSHEETINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff538492)構造体し、の実装にその情報を返す[**IDIGameCntrlPropSheet::GetPageInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff540026)と[ **IDIGameCntrlPropSheet::GetSheetInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff540029)それぞれします。

プロパティ シートのページの生成を行う、**プロパティ シート**関数。 この関数のすべての動作は、プロパティ シートのページに固有です。 たとえば、プロパティ シートのページには、受信した最大のダイアログ テンプレートが反映されます。 ユーザーは、1 つのページを作成します。 その関連テンプレートは非常に小さい場合は、これは表示されたダイアログのサイズに直接反映されます。

ダイアログ テンプレートも visual 配置と、ページ上のコントロールの中央揃えを検討する際に注意してください。 たとえば、場合は、ユーザーがページの中央揃えにする指定された項目が含まれている 2 つのページを作成します。 中央揃えにする 1 つの項目の幅は 200 ダイアログ単位 (Dlu)もう 1 つは 100 単位です。 このような場合は、ページで、後者のアイテムは中央に表示されません。 代わりに、コントロールが、テンプレートと追加の空白文字を中央揃え (または可能性があるとは灰色) より限られたページの幅に追加されます。 すべて使用されていない場合でも、同じサイズのダイアログ テンプレートを作成する必要があります。 (の詳細については、**プロパティ シート**関数を Microsoft Win32 SDK を参照してください)。
