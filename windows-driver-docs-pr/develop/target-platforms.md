---
ms.assetid: EB2264A4-BAE8-446B-B9A5-19893936DDCA
title: ドライバー リファレンス ページでのターゲット プラットフォーム
description: Microsoft ドライバー リファレンス ページの下部にある要件ブロックには、ターゲット プラットフォームという名前のエントリが表示されます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84e824f0536b8aa039a64db8227bb7cea3b65178
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270455"
---
# <a name="target-platform-on-driver-reference-pages"></a>ドライバー リファレンス ページでのターゲット プラットフォーム

Microsoft ドライバー リファレンス ページの下部にある要件ブロックには、**ターゲット プラットフォーム**という名前のエントリが表示されます。 次の行は、ページが適用される Windows のエディションの一覧です。

次に示すのは、このようなエントリの例です。

![要件ブロックでターゲット プラットフォームがユニバーサルに設定されている](images/TargetPlatform.png)

**[ターゲット プラットフォーム]** に指定された値は、Visual Studio の **[構成プロパティ]、[ドライバーの設定]、[全般]** の下にある **[ターゲット プラットフォーム]** プロパティで使用できる値にマップされます。  **Windows ドライバー**では、 **[ユニバーサル]** でターゲット プラットフォームを指定する任意の DDI を使用できます。

**ターゲット プラットフォーム**に対して表示される値とその意味を、次に説明します。

|用語|説明|
|--- |--- |
|ユニバーサル|Windows ドライバーのドライバー バイナリは、このデバイス ドライバー インターフェイス (DDI) を呼び出すことができます。

Windows ドライバーは、次に示す Windows 10 のユニバーサル Windows プラットフォーム (UWP) ベース エディションで動作します。

*   Windows 10 デスクトップ エディション (Home、Pro、Enterprise)
*   S モードの Windows 10
*   Windows 10 IoT Core
*   Windows Server 2016

詳細については、「[Windows ドライバーの概要](getting-started-with-windows-drivers.md)」を参照してください。| |デスクトップ|Windows 10 デスクトップ エディションまたは Windows Server 2016 のドライバー バイナリは、この DDI を呼び出すことができます。|



