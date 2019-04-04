---
title: IoSpy と IoAttack でファジー テストを実行する方法
description: このトピックでは、IoSpy IoAttack ツールを使用して、ファジー テストを実行する方法を説明します
ms.assetid: f800e962-2a0f-4039-a479-395a62428b06
ms.date: 07/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 646c9b4592b3cc23fde1305a14398d761e46f026
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577978"
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

# <a name="how-to-perform-fuzz-tests-with-iospy-and-ioattack"></a>IoSpy と IoAttack でファジー テストを実行する方法


使用して、ファジー テストを実行する[IoSpy](iospy.md)と[IoAttack](ioattack.md)次の操作を行います。

1.  インストール[IoSpy](iospy.md):

    IoSpy をインストールし、特定のデバイスにファジー テストを有効にするには実行、**を有効にする I/O スパイ**をテストします。 *DQ*パラメーターは、IoSpy フィルター ドライバーがインストールされているデバイスを制御します。

2.  指定したデバイス IOCTL および WMI のテストを実行します。

    テスト システムを再起動した後[IoSpy](iospy.md)ファジー テストの有効化されたデバイスに IOCTL および WMI の要求をフィルター処理する準備ができました。 IOCTL を今すぐ行うことが必要し、するすべてのテストを使用してこれらのデバイス用のドライバーでの WMI コード パスが適切です。 これにより、これらの IOCTL および WMI の要求に基づいてできるだけ多くの詳細を記録する IoSpy できます。 IoSpy でこれらの詳細を保存する、 [IoSpy データファイル](iospy.md)します。

3.  IoSpy をアンインストールします。

    IOCTL および WMI のコード パスを完全に演習するが後、ファジー テストを実行する IoAttack を実行する前に IoSpy をまずアンインストールする必要があります。 アンインストールする[IoSpy](iospy.md)、実行、 **I/O スパイを無効にする**をテストします。

    このコマンドを削除、 [IoSpy](iospy.md)ファジー テストを有効にしていたすべてのデバイスからのフィルター ドライバー。 コマンドを実行すると、メモリから IoSpy フィルター ドライバーをアンロードするために、テスト システムを再起動します。

    **注**  IoSpy をアンインストールすると、IoSpy データ ファイルは削除されません。 このファイルの場所が設定されて、 *DFD*パラメーターを**I/O スパイを有効にする**をテストします。 既定の場所は %systemdrive%\\DriverTest\\IoSpy します。 詳細については、[IoSpy データファイル](iospy.md)を参照してください。

     

4.  実行[IoAttack](ioattack.md):

    テスト システムを実行して、ファジー テストを実行する準備ができました、 **I/O 攻撃の実行**をテストします。 IoAttack を実行する方法の詳細については、[IoAttack](ioattack.md)を参照してください。

    **注**  ドライバーの IOCTL および WMI インターフェイスのアクセス権限を確認するために実行する必要があります[IoAttack](ioattack.md) guest アカウントや管理者などのさまざまな権限を持つアカウントアカウント。

     

 

 





