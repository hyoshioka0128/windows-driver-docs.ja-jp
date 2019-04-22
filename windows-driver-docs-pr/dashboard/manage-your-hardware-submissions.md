---
title: ハードウェア提出の管理
description: パートナー センターのハードウェア申請の管理
ms.assetid: C4C3C56F-8E92-4CB1-A57B-942E466ECD3D
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c2649bac3fe5edf312fa80683ba72d674e4e51b
ms.sourcegitcommit: 3508ab1c06671ac52e446aa2556b53f978ef6d83
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2019
ms.locfileid: "59586380"
---
# <a name="managing-hardware-submissions-in-the-partner-center"></a>パートナー センターでのハードウェア申請の管理

Windows 10 の Windows ハードウェア互換性プログラム (以前のバージョンの Windows の場合は認定プログラム) に製品を申請した後で、ダッシュボードを使用して製品を管理できます。

## <a name="find-a-hardware-submission"></a>ハードウェア申請を検索する

「[Find hardware submission (ハードウェア申請を検索する)](find-hardware-submission.md)」をご覧ください。

## <a name="update-an-hck-or-hlk-hardware-submission-using-the-driver-update-acceptable-dua-process"></a>Driver Update Acceptable (DUA) プロセスを使って HCK または HLK ハードウェア申請を更新する

> [!Note]
> DUA 申請は、初回の申請でしか作成できません。
> - 他の会社と共有されている DUA 申請では、1 回の DUA 申請で 1 つの DUA を処理できないため、[Download DUA Shell]\(DUA シェルのダウンロード\) ボタンは表示されません。

DUA シェルから DUA 申請を作成する方法については、「[ドライバーのみの更新プログラム パッケージの作成](https://docs.microsoft.com/windows-hardware/test/hlk/user/create-a-driver-only-update-package)」をご覧ください。

## <a name="registering-an-extensionid"></a>ExtensionId を登録する

拡張 INF の署名を申請すると、ダッシュボードでは、指定した **ExtensionId** が以前に別のアカウントで登録されているかどうかが確認されます。
そうであった場合は、別の ID の指定を求めるメッセージが表示されます。 そうでなかった場合は、ダッシュボードでそれがお使いのアカウントと関連付けられます。

**ExtensionId** を指定する方法について詳しくは、「[拡張 INF ファイルの使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)」をご覧ください。

申請に使用できるのは、アカウントに登録されている ExtensionID のみです。

## <a name="related-topics"></a>関連トピック

- [新しいハードウェア申請の作成](create-a-new-hardware-submission.md)
- [複数の Windows バージョンで Microsoft によって署名されたドライバーを取得する](get-drivers-signed-by-microsoft-for-multiple-windows-versions.md)
- [ドライバーのフライティング](driver-flighting.md)
