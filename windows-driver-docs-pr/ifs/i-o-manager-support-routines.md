---
title: I/o マネージャーのサポートルーチン
description: I/o マネージャーのサポートルーチン
ms.assetid: f0b0099e-f920-4287-9e5d-e0fd4241f100
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: decd2ec8992bc8432e18d729c0ae1a8d3c1b4902
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841214"
---
# <a name="io-manager-support-routines"></a>I/o マネージャーのサポートルーチン

次のシステム指定の i/o マネージャー関数とマクロは、カーネルモードのファイルシステムとファイルシステムフィルター (ミニフィルターまたはレガシフィルター) ドライバーによって呼び出すことができます。 デバイスドライバーでは使用できません。 これらはアルファベット順に表示されます。

ここに記載されているルーチンに加えて、ファイルシステムとフィルタードライバーは、 *ntifs*で宣言されている[Windows カーネルリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_kernel/)セクションで説明されている Io*Xxx** * ルーチンを呼び出すこともできます。

**ヘッダーファイル:** *ntifs*

**プレフィックス: Io**_xxx_、 **IsReparseTag**_xxx_

| 関数またはマクロ | 説明 |
| ----------------- | ----------- |
| **IoAcquireVpbSpinLock** | ボリュームパラメーターブロック (VPB) のスピンロックを取得します。 |
| **IoAttachDeviceToDeviceStackSafe** | 呼び出し元のデバイスオブジェクトを、ドライバースタック内の最上位のデバイスオブジェクトにアタッチします。 |
| **IoCancelFileOpen** | は、ファイルシステムフィルタードライバーによって使用され、ファイルシステムドライバーによってフィルタードライバーのデバイススタックで開かれたファイルを閉じることができます。 |
| **IoCheckDesiredAccess** | システム用に予約されています。 |
| **IoCheckEaBufferValidity** | 指定された拡張属性 (EA) バッファーが有効かどうかを確認します。 |
| **IoCheckFunctionAccess** | システム用に予約されています。 |
| **IoCheckQuerySetFileInformation** | システム用に予約されています。 |
| **IoCheckQuerySetVolumeInformation** | システム用に予約されています。 |
| **IoCheckQuotaBufferValidity** | 指定されたクォータバッファーが有効かどうかを確認します。 |
| **IoCreateFileEx** | 新しいファイルまたはディレクトリを作成するか、既存のファイル、デバイス、ディレクトリ、またはボリュームを開いて、呼び出し元にファイルオブジェクトのハンドルを与えます。 ファイルシステムフィルタードライバー (レガシフィルタードライバー) は、このルーチンを呼び出します。 |
| **Iocreatefilの場合は、デバイスを Ioint にします。** | ファイルシステムフィルタードライバーが、指定されたデバイスオブジェクトおよびファイルシステムの下にあるフィルターに対してのみ作成要求を送信するために使用されます。 |
| **IoCreateStreamFileObject** | 新しいストリームファイルオブジェクトを作成します。 |
| **IoCreateStreamFileObjectEx** | 新しいストリームファイルオブジェクトを作成します。 |
| **IoCreateStreamFileObjectEx2** | ターゲットデバイスオブジェクトの create オプションを使用して、新しいストリームファイルオブジェクトを作成します。 |
| **Iocreatestreamfileite Tlite** | 新しいストリームファイルオブジェクトを作成しますが、IRP_MJ_CLEANUP 要求がファイルシステムのドライバースタックに送信されることはありません。 |
| **IoEnumerateDeviceObjectList** | ドライバーのデバイスオブジェクトリストを列挙します。 |
| **IoEnumerateRegisteredFiltersList** | システムに登録されているファイルシステムフィルタードライバーを列挙します。 |
| **IoFastQueryNetworkAttributes** | システム用に予約されています。 |
| **IoGetAttachedDevice** | 指定されたデバイスに関連付けられている最上位レベルのデバイスオブジェクトへのポインターを返します。 |
| **IoGetBaseFileSystemDeviceObject** | システム用に予約されています。 |
| **IoGetDeviceAttachmentBaseRef** | ファイルシステムまたはデバイスドライバースタック内の最下位レベルのデバイスオブジェクトへのポインターを返します。 |
| **IoGetDeviceToVerify** | 指定されたスレッドの i/o 要求のターゲットである、リムーバブルメディアデバイスを表すデバイスオブジェクトへのポインターを返します。 |
| **IoGetDiskDeviceObject** | 特定のファイルシステムボリュームデバイスオブジェクトに関連付けられているディスクデバイスオブジェクトへのポインターを取得します。 |
| **IoGetLowerDeviceObject** | ドライバースタック上の次の下位レベルのデバイスオブジェクトへのポインターを返します。 |
| **IoGetOplockKeyContext** | ファイルオブジェクトのターゲット oplock キーコンテキストを返します。 |
| **IoGetOplockKeyContextEx** | ファイルオブジェクトの親とターゲットの oplock キーコンテキストを返します。 |
| **IoGetRequestorProcess** | 指定された i/o 操作を最初に要求したスレッドのプロセスポインターを返します。 |
| **IoGetRequestorProcessId** | 指定された i/o 操作を最初に要求したスレッドの一意の32ビットプロセス ID を返します。 |
| **IoGetRequestorSessionId** | 指定された i/o 操作を最初に要求したプロセスのセッション ID を返します。 |
| **IoGetTopLevelIrp** | 現在のスレッドの TopLevelIrp フィールドの値を返します。 |
| **IoGetTransactionParameterBloc** | トランザクションファイル操作のトランザクションパラメーターブロックを返します。 |
| **IoInitializeDriverCreateContext** | IO_DRIVER_CREATE_CONTEXT 型の呼び出し元割り当て変数を初期化します。 |
| **Ioinitializeの優先順位情報** | IO_PRIORITY_INFO 型の構造体を初期化します。 |
| **IoIsFileObjectIgnoringSharing** | ファイル共有のアクセスチェックを無視するオプションを使用して、ファイルオブジェクトが設定されているかどうかを判断します。 |
| **IoIsFileOpenedExclusively** | システム用に予約されています。 |
| **Ioisfileのリモート** | 指定されたファイルオブジェクトがリモート作成要求用かどうかを判断します。 |
| **IoIsOperationSynchronous** | 特定の IRP が、同期または非同期の i/o 要求を表すかどうかを判断します。 |
| **IoIsSystemThread** | 特定のスレッドがシステムスレッドであるかどうかを確認します。 |
| **IoIsValidNameGraftingBuffer** | システム用に予約されています。 |
| **IoPageRead** | システム用に予約されています。 |
| **Ioqueueます。** | システム用に予約されています。 |
| **IoQueryFileDosDeviceName** | ファイルの MS-DOS デバイス名を取得します。 |
| **IoQueryFileInformation** | システム用に予約されています。 |
| **IoQueryVolumeInformation** | システム用に予約されています。 |
| **IoRegisterFileSystem** | ファイルシステムのコントロールデバイスオブジェクトをグローバルファイルシステムキューに追加します。 |
| **IoRegisterFsRegistrationChange** | ファイルシステムがアクティブなファイルシステムとして登録または登録解除するたびに呼び出される、ファイルシステムフィルタードライバーの通知ルーチンを登録します。 |
| **IoRegisterFsRegistrationChangeEx** | ファイルシステムがアクティブなファイルシステムとして登録または登録解除するたびに呼び出される、ファイルシステムフィルタードライバーの通知ルーチンを登録します。 |
| **IoRegisterFsRegistrationChangeMountAware** | ファイルシステムフィルタードライバーの通知ルーチンを登録します。 この通知ルーチンは、ファイルシステムがアクティブなファイルシステムとして登録または登録解除を行うたびに呼び出されます。 |
| **IoReleaseVpbSpinLock** | ボリュームパラメーターブロック (VPB) のスピンロックを解放します。 |
| **IoReplaceFileObjectName** | ファイルオブジェクトの名前を置き換えます。 |
| **IoSetDeviceToVerify** | 検証するデバイスオブジェクトを指定します。 指定されたデバイスオブジェクトは、リムーバブルメディアデバイスを表します。 |
| **IoSetFileObjectIgnoreSharing** | ファイル共有のアクセスチェックを無視するようにファイルオブジェクトを設定します。 |
| **IoSetFileOrigin** | 指定されたファイルオブジェクトがリモート作成要求用かどうかを指定します。 |
| **IoSetInformation** | システム用に予約されています。 |
| **IoSetTopLevelIrp** | 現在のスレッドの*TopLevelIrp*フィールドの値を設定します。 |
| **IoSynchronousPageWrite** | システム用に予約されています。 |
| **IoThreadToProcess** | 指定されたスレッドのプロセスへのポインターを返します。 |
| **IoUnregisterFileSystem** | ファイルシステムのコントロールデバイスオブジェクトをグローバルファイルシステムキューから削除します。 |
| **IoUnregisterFsRegistrationChange** | ファイルシステムフィルタードライバーのファイルシステムの登録変更通知ルーチンの登録を解除します。 |
| **IoVerifyVolume** | 指定されたリムーバブルメディアデバイスにボリューム検証要求を送信します。 |
| **IsReparseTagMicrosoft** | 再解析ポイントタグが Microsoft 再解析ポイントを示すかどうかを判断します。 |
| **IsReparseTagNameSurrogate** | タグに関連付けられた再解析ポイントが、ボリュームマウントポイントなど、別の名前付きエンティティのサロゲートであるかどうかを判断します。 |
| **IsReparseTagValid** | システム用に予約されています。 |
