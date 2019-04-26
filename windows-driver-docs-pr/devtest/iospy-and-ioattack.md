---
title: IoSpy と IoAttack
description: IoSpy と IoAttack
ms.assetid: 4cc5bf5c-f9e4-43d4-8532-dd7813b6f2a0
ms.date: 07/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: a8ee226ee52ab9754fc21be11fa9406dea3ce144
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356520"
---
> [!NOTE]
> IoSpy と IoAttack は Windows 10 バージョン 1703 後は WDK に含まれて使用できなくします。
>
> これらのツールを別の方法として、HLK で使用可能なファジー化のテストを使用して検討してください。 次に考慮すべきいくつか示します。
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
> 使用することも、[カーネル同期遅延ファジー テスト](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-synchronization-delay-fuzzing)Driver Verifier に含まれます。
>


# <a name="iospy-and-ioattack"></a>IoSpy と IoAttack


IoSpy と IoAttack、IOCTL および WMI を実行するツールがカーネル モード ドライバーのテストをファジー化です。 これらのツールを使用すると、そのドライバーの IOCTL ことを確認できるし、データ バッファーとバッファーの長さが正しく検証 WMI コード。 これにより、システムが不安定につながるバッファー オーバーランを回避します。

*ファジー テスト*と呼ばれる、ランダム データでドライバーを表示します。*ファジー*、ドライバー内で欠陥を決定するためにします。 ファジー テスト IOCTL または WMI インターフェイス上では、新しいではありません。 ただし、ほとんどのテスト スイートでは、ジェネリック*ブラック_ボックス*ファジー テストのみドライバーの IOCTL または WMI インターフェイスへの外部アクセスを確認します。 または、テスト、ドライバー内で特定の IOCTL および WMI パスに書き込まれます。

IoSpy と IoAttack 使用の詳細は、*ホワイト ボックス*ファジー テストする方法。 ファジー テストでデバイスを有効にすると、IoSpy は、デバイスのドライバーに送信された IOCTL および WMI の要求をキャプチャし、データ ファイル内でこれらの要求の属性を記録します。 IoAttack: このデータ ファイルからの属性の読み取りし、これらの属性を使用して*ファジー*、またはランダムにドライバーに送信する前に、さまざまな方法で IOCTL または WMI 要求を変更します。 これはにより IOCTL または WMI に固有のテストを記述することがなく、ドライバーのバッファーの検証コードへのエントリではさらにできます。

IoSpy と IoAttack は、Windows Vista または Windows オペレーティング システムの以降のバージョンを実行するシステムでサポートされます。 これらのツールは、同様の一部として WDK に含まれるの一部、[デバイス基礎テスト](device-fundamentals-tests.md)を参照してください[侵入テスト (デバイスの基本)](coverage-tests--device-fundamentals-.md)します。 これらのテストを選択することができます、**追加または削除するドライバーのテスト**ダイアログ ボックスの Basic\\デバイス基礎\\侵入\\IoSpy と攻撃のフォルダー。

**重要な**   IoSpy と IoAttack をカーネル モードのデバッグを既に準備しているテスト システムで実行する必要があります。

 

ここでは、次のトピックについて説明します。

[IoSpy](iospy.md)

[IoAttack](ioattack.md)

[IoSpy IoAttack と実行のファジー テストする方法](how-to-perform-fuzz-tests-with-iospy-and-ioattack.md)

 

 





