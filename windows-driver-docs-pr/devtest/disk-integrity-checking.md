---
title: ディスク整合性チェック
description: ディスク整合性チェック
ms.assetid: bb838594-637c-4fc4-b2ec-964b69faabcf
keywords:
- ディスクの整合性チェック機能 WDK Driver Verifier
- ディスク記憶域精度 WDK Driver Verifier
- 記憶域精度 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19f7a4deb4a694ff39be7d0d2b694e9a1aad8dea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329680"
---
# <a name="disk-integrity-checking"></a>ディスク整合性チェック


## <span id="ddk_disk_integrity_verification_tools"></span><span id="DDK_DISK_INTEGRITY_VERIFICATION_TOOLS"></span>


Driver Verifier のディスクの整合性チェック機能は、ディスクが正確に情報を格納しているかどうかを決定するすべてのハード ディスク アクセスを監視します。 ディスク上のデータは、変更が表示されたら、バグ チェックが発行されます。

このドライバーの検証オプションでは、Windows Server 2003 で導入されたされ、Windows 7 以降では、オプションとして削除されました。

### <a name="span-idhowdiskintegritycheckingworksspanspan-idhowdiskintegritycheckingworksspanhow-disk-integrity-checking-works"></a><span id="how_disk_integrity_checking_works"></span><span id="HOW_DISK_INTEGRITY_CHECKING_WORKS"></span>ディスクの整合性チェックの動作

ディスクの整合性チェックをアクティブ化すると、コンピューターに接続された物理ディスクの一部またはすべてを確認することもできます。

Driver Verifier は、監視を開始 Windows とそのドライバーが読み込まれるとすぐにすべての読み取りし、書き込みアクションはこれらのドライブに加えられました。 Driver Verifier は、各セクターにアクセスし、この値を保存するには、CRC (巡回冗長検査) チェックサム値を計算します。 次回このセクターにアクセスすると、Driver Verifier は、このチェックサムが再計算され、以前の値を比較します。

チェックサム値が変更された場合は、ディスクの整合性に問題が--欠陥のある情報は、またはディスクのメディアは、最後のアクセスが行われた後に、その内容に変更が読み取りのいずれかの操作を返します。 このような場合は、Driver Verifier の問題のバグは、パラメーター 1 と等しい 0xA0 0xC4 を確認します。 その他のパラメーターは、以下のデバイスと、エラーが発生したセクターのデバイス オブジェクトを使用して、要求を行う IRP を特定します。 詳細については、次を参照してください。 [**バグ チェック 0xC4** ](https://msdn.microsoft.com/library/windows/hardware/ff560187) (ドライバー\_VERIFIER\_検出\_違反)。

### <a name="span-idperformanceissuesspanspan-idperformanceissuesspanperformance-issues"></a><span id="performance_issues"></span><span id="PERFORMANCE_ISSUES"></span>パフォーマンスの問題

ディスクの整合性チェック機能により、perceptibly 低速のハード ディスク アクセス。 コンピューターが RAM 不足の場合は、このパフォーマンスの低下は、さらに大きなです。 ディスクの整合性チェックを使用して、ディスクの問題を調査するが、ときにドライバーをテストするドライバーの検証ツールを実行しているときにアクティブにしません。

**注**  ディスクの整合性チェック機能がクラスター化共有ディスクを使用するシステムで動作するものはありません。 このようなシステムでディスクの整合性チェック機能を有効にすると、ディスクの整合性チェック誤ってが生じるバグ チェックが発生します。 そのため、共有ディスクをクラスター化されたシステムでこの機能を有効にしないを強くお勧めします。
さらに、クラスター化されていないディスクを備えたシステムで false バグ チェックにつながる可能性のあるいくつかの状況があります。 このような状況は次のとおりです。

-   実行中の書き込みバッファー メモリに書き込みます

-   同時実行中は、読み取りし、書き込み同一のセクターに

 

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、ディスクの整合性チェック オプションをアクティブ化することができます。 ドライバー検証マネージャーを使用して、どのディスクが検証を指定できます。 コマンドラインを使用する場合は、すべてのディスクが検証されます。 詳細については、次を参照してください。[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)します。

-   **コマンドラインで**

    によって表されるディスクの整合性チェック オプション、コマンド行で、 **/ディスク**パラメーター。 次に、例を示します。

    ```
    verifier /disk /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。 任意のバージョンの Windows 上のコンピューターを再起動しなくても、ディスクの整合性チェック オプションをアクティブ化することはできません。

-   **ドライバー検証マネージャーを使用します。**
    1.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    2.  選択**完全な一覧から個々 の設定を選択します。** します。
    3.  選択 (チェック)**ディスクの整合性チェック**します。

 

 





