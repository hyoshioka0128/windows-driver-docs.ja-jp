---
title: IoSpy と IoAttack
description: IoSpy と IoAttack
ms.assetid: 4cc5bf5c-f9e4-43d4-8532-dd7813b6f2a0
ms.date: 07/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: fcf4b33dc20e9e668a39f2ae7c1deceb94967011
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235288"
---
# <a name="iospy-and-ioattack"></a>IoSpy と IoAttack

> [!NOTE]
> IoSpy と Iospy は、Windows 10 バージョン1703以降の WDK では利用できなくなりました。
>
> これらのツールの代わりに、HLK で使用可能なファジーテストの使用を検討してください。 次に、考慮すべき点をいくつか示します。
> 
> [DF - ランダム IOCTL のファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/236b8ad5-0ba1-4075-80a6-ae9dafb71c94)
>
> [DF - サブオープンのファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/92bf534e-aa48-4aeb-b3cd-e46fb7cc7d80)
>
> [DF - 0 長バッファー FSCTL のファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/5f5f6c7e-d5db-4ff1-8cee-da47203ab070)
>
> [DF - ランダム FSCTL のファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/e529e34e-076a-4978-926f-7eca333e8f4d)
>
> [DF - Misc API のファジー テスト (信頼性)](https://docs.microsoft.com/windows-hardware/test/hlk/testref/fb305d04-6e8c-4dfc-9984-9692df82fbd8)
>
> また、ドライバー検証ツールに含まれている[カーネル同期遅延ファジー化](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-synchronization-delay-fuzzing)を使用することもできます。
>

IoSpy と Iospy は、カーネルモードドライバーで IOCTL および WMI ファジーテストを実行するツールです。 これらのツールを使用すると、ドライバーの IOCTL および WMI コードによってデータバッファーとバッファー長が正しく検証されるようにすることができます。 これにより、システムが不安定になる可能性があるバッファーオーバーランを回避できます。

*ファジーテスト*では、ドライバー内の欠陥を特定するために、ランダムなデータ (*ファジー*) を使用してドライバーを提示します。 IOCTL インターフェイスまたは WMI インターフェイスに対するファジーテストは新しいものではありません。 ただし、ほとんどのテストスイートは、一般的な*ブラックボックス*のファジーテストで、ドライバーの ioctl インターフェイスまたは wmi インターフェイスへの外部アクセスだけを検証するか、ドライバー内の特定の IOCTL および wmi パスをテストするように記述されています。

IoSpy と Iospy は、ファジーテストのための*ホワイトボックス*アプローチの多くを使用します。 デバイスでファジーテストが有効になっている場合、デバイスのドライバーに送信された IOCTL および WMI 要求をキャプチャし、それらの要求の属性をデータファイル内に記録します。 その後、IoAttack は、このデータファイルから属性を読み取り、これらの属性を使用して IOCTL または WMI 要求をドライバーに送信する前に、さまざまな方法でそれらを*ファジー*化またはランダムに変更します。 これにより、IOCTL または WMI 固有のテストを記述することなく、ドライバーのバッファー検証コードにさらに入力できます。

IoSpy と Iospy は、windows Vista 以降のバージョンの Windows オペレーティングシステムを実行するシステムでサポートされています。 これらのツールは、[デバイスの基本テスト](device-fundamentals-tests.md)の一環として、の一部として WDK に含まれています。「[侵入テスト (デバイスの基礎)](coverage-tests--device-fundamentals-.md)」を参照してください。 これらのテストを選択するには、[**ドライバーテストの追加または削除**] ダイアログボックスの [基本 \\ デバイスの基本 \\ 侵入 \\ iospy & 攻撃フォルダー] をクリックします。

**重要**   IoSpy と Iospy は、以前にカーネルモードデバッグ用に準備されたテストシステムで実行する必要があります。

 

ここでは、次のトピックについて説明します。

[IoSpy](iospy.md)

[IoAttack](ioattack.md)

[IoSpy と Iospy でファジーテストを実行する方法](how-to-perform-fuzz-tests-with-iospy-and-ioattack.md)

 

 





