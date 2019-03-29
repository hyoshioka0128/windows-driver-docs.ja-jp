---
title: IoAttack
description: 侵入テスト (デバイスの基本) テストには、I/O 攻撃の実行は、ファジー テストを実行します。
ms.assetid: ae0eda5c-534e-44c2-a997-66fe1337ca9f
ms.date: 07/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 75f298a6d03b2261bbe8a3d977e3f1240ca8321e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582508"
---
# <a name="ioattack"></a>IoAttack

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


[侵入テスト (デバイスの基本)](penetration-tests--device-fundamentals-.md)テスト**I/O 攻撃の実行**ファジー テストを実行します。 **I/O 攻撃の実行**用途のテスト、 [IoSpy データ ファイル](iospy.md)IoSpy を通じて、テスト システムで作成された以前。

テスト システムで IoAttack を実行する前に、次の操作を行う必要があります。

-   テスト コンピューターでカーネル モードのデバッグを有効にします。 テストのためにコンピューターを構成するときにこれを参照してください[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)、または[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8)](https://msdn.microsoft.com/library/windows/hardware/hh698272)します。

-   実行、 **Driver Verifier を有効にするテスト**有効にする[Driver Verifier](driver-verifier.md)オプション ドライバー スタック内のドライバーのすべてのデバイスをテストできます。 具体的には、有効にしてください、[特別なプール](special-pool.md)オプション。 **追加または削除するドライバー テスト** ダイアログ ボックスで、 **Driver Verifier を有効にするテスト**すべてのテストの\\Driver Verifier。 「[Visual Studio を使って実行時にドライバーをテストする方法](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)」をご覧ください。 選択して、テストとツールのパラメーターの構成については、次を参照してください[を選択して、デバイスの基本テストを構成する方法。](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

-   削除[IoSpy](iospy.md)テスト システムからです。 これを行うには、実行、 **I/O スパイを無効にする**をテストします。

次の手順のいずれかが実行されている場合は、IoAttack を実行する前に、テスト システムを再起動する必要があります。

ファジー テストを実行する方法の詳細については、次を参照してください。 [IoSpy IoAttack と実行のファジー テスト方法](how-to-perform-fuzz-tests-with-iospy-and-ioattack.md)します。

 

 





