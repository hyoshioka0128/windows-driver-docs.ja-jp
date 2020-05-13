---
title: IoSpy と IoAttack でファジー テストを実行する方法
description: このトピックでは、IoSpy および Iospy ツールを使用してファジーテストを実行する方法について説明します。
ms.assetid: f800e962-2a0f-4039-a479-395a62428b06
ms.date: 07/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5376d23b3cfaf6b67e045415c8fdb12b711eb0de
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235300"
---
# <a name="how-to-perform-fuzz-tests-with-iospy-and-ioattack"></a>IoSpy と IoAttack でファジー テストを実行する方法

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


[Iospy](iospy.md)と[iospy](ioattack.md)を使用してファジーテストを実行するには、次の手順を実行します。

1.  [Iospy](iospy.md)のインストール:

    IoSpy をインストールし、特定のデバイスでファジーテストを有効にするには、 **enable I/o Spy**テストを実行します。 *DQ*パラメーターは、iospy フィルタードライバーがインストールされているデバイスを制御します。

2.  指定されたデバイスで IOCTL および WMI テストを実行します。

    テストシステムを再起動した後、 [Iospy](iospy.md)は、IOCTL および WMI 要求を、ファジーテストが有効になっているデバイスにフィルター処理する準備ができています。 ここで、適切なテストを使用して、これらのデバイスのドライバーで IOCTL および WMI コードパスを実行する必要があります。 これにより、IoSpy は、これらの IOCTL および WMI 要求に基づいて、可能な限り多くの詳細情報を記録することができます。 IoSpy は、これらの詳細を[Iospy データファイル](iospy.md)に保存します。

3.  IoSpy のアンインストール:

    IOCTL および WMI コードパスを完全に実行したら、IoSpy を事前にアンインストールしてから、ファジーテストを実行する必要があります。 [Iospy](iospy.md)をアンインストールするには、 **Disable i/o spy**テストを実行します。

    このコマンドは、ファジーテストが有効にされたすべてのデバイスから[Iospy](iospy.md)フィルタードライバーを削除します。 コマンドを実行した後、メモリから IoSpy フィルタードライバーをアンロードするために、テストシステムを再起動します。

    **メモ**   IoSpy をアンインストールしても、IoSpy データファイルは削除されません。 このファイルの場所は、 *DFD*パラメーターによって、 **Enable i/o Spy**テストに設定されます。 既定の場所は% SystemDrive% \\ drivertest \\ iospy です。 詳細については、「 [Iospy データファイル](iospy.md)」を参照してください。

     

4.  [Ioattack](ioattack.md)を実行する:

    テストシステムは、**実行 I/o 攻撃**テストを実行して、ファジーテストを実行する準備ができました。 IoAttack の実行方法の詳細については、「 [ioattack](ioattack.md)」を参照してください。

    **メモ**   お使いのドライバーの IOCTL および WMI インターフェイスのアクセス特権を確認するには、ゲストアカウントや管理者アカウントなど、さまざまな権限を持つ[Ioattack](ioattack.md)アカウントを実行する必要があります。

     

 

 





