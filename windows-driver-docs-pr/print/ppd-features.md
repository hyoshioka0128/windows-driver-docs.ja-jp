---
title: PPD 機能
description: PPD 機能
ms.assetid: ee78031a-2138-4d0c-ac8a-5328aa54d904
keywords:
- PPD ファイル WDK Pscript
- 非 PPD WDK Pscript を機能します。
- ドライバーは、WDK Pscript を機能します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fddd9d92defca0ae15f3c5e0829206ce7651bba4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559927"
---
# <a name="ppd-features"></a>PPD 機能





PPD 機能が PPD ファイル内で定義されている **\*OpenUI**/**\*CloseUI**キーワードの組み合わせを構造体と同様に扱われる特定の PPD キーワードPscript ドライバー。 **EnumFeatures**を一覧表示、  **\*LeadingEdge**と **\*UseHWMargins**キーワード、PPD内で定義されていない **\*OpenUI**/**\*CloseUI**キーワードの組み合わせを構造体します。 その結果、 **GetOptions**と**SetOptions**メソッドは、機能の一覧に表示される場合にこれらのキーワードを無視します。 PPD 機能またはオプションのキーワードは大文字小文字を区別します。

**SetOptions** PPD の特定の機能を特別な方法で処理します。

-   プリンターの PPD ファイルが含まれている場合、  **\*OutputOrder**キーワードの機能と**SetOptions**が呼び出され、この機能のオプションの選択を変更する、 **%pageorder**ドライバー機能の設定は、新しい出力順序が一致するように変更します。 これは、スプーラーが不要なページの順序のシミュレーションを実行することを防止するためです。

-   プリンターの PPD ファイルが含まれている場合、  **\*OutputBin**キーワードの機能と**SetOptions**の現在の設定を変更するには、この機能と変更の原因のためのオプション選択のために呼び出される **%pageorder**逆の順序付け、プリンターのページを使用するドライバーの機能と **%metafilespooling**は"False" **%metafilespooling**されます"True"にリセットされます。

-   スプーラー EMF スプールが有効にすると、 **Collate** "True"に設定されている (いずれかのパブリックの部分に直接で設定できます、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)構造体またはを呼び出すことによって**SetOptions** PPD の **\*Collate**キーワードの機能) が、 **Collate**機能は現在使用できません、 **%MetafileSpooling**は"False" **%metafilespooling**は"True"にリセットされます。 これは、すべての設定が要求されたときに、 **SetOptions**呼び出しが適用されます。

-   場合**双方向**シンプレックスに設定されている (DEVMODE 構造体のまたは呼び出すことによって、パブリックの部分で直接かで設定できます**SetOptions** PPD の **\*双方向**キーワードの機能) が **%pagepersheet** 「小冊子」に設定し、 **%pagepersheet** 「2」に変更されます。 これは、すべての設定が要求されたときに、 **SetOptions**呼び出しが適用されます。

 

 




