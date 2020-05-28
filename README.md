# Autodrive AirSim

Microsoft tarafından bilgisayarla görü ve reinforcement ile öğrenme gibi yapay zeka araştırmaları için geliştirilmiş özel bir simülatördür. Araba, drone gibi çeşitli kara ve hava alanlarında kullanılabilir. 

Airsim, Unreal Engine plugin'i olarak tasarlanmıştır ve hala geliştirme aşamasında olsa da Unity versiyonu da mevcuttur.

## Versiyon
v1.3.1 - Windows

## Kurulum

### Windows

AirSim bir Unreal plugin’i olarak tasarlanmıştır. Dolayısıyla kendi başına çalışamaz ve bir Unreal projesine (environment) ihtiyaç duyar. Airsim’i build edip test etmek 2 aşamadan oluşur:
* Build the plugin
* Deploy plugin in Unreal project and run the project.

Bu nedenle öncelikle bilgisayarımıza Unreal Engine (UE >= 4.22) kurmamız gerekir. Bunun için:
1.	Öncelikle Epic Games Launcher’ı indirin. Unreal Engine açık kaynak kodludur ama indirmek için Unreal Engine sitesinde hesap açmanız gerekmektedir. Hesap açtıktan sonra aşağıdaki linkten Epic Games launcher’ı indirin.
https://www.unrealengine.com/en-US/download
2.	İndirme işlemi tamamlanınca Epic Games launcher’ı açın ve üst taraftaki panelde bulunan “Library” tabını açın ve Engine Versions kısmındaki + butonuna tıklayarak Unreal 4.24 versionunu indirin.
3.	Daha sonrasında Airsim’i build etmek için Visual Studio 2019’u indirin. 
“Desktop Development with C++ “ ile “Windows 10 SDK 10.0.18362” seçeneklerinin seçili olduğundan emin olun.
Not: Eğer Airsim’deki PythonClient API’sini kullanacaksanız “Development with Python” paketini de seçin.

4.	İndirme tamamlandıktan sonra “Developer Command Prompt for VS 2019” ini açın ve Airsim reposunu clone’layın ve build edin.
git clone https://github.com/Microsoft/AirSim.git
cd Airsim
build.cmd

Build işleminden sonra, Unreal\Plugins klasöründe herhangi bir Unreal projesine bırakılabilen kullanıma hazır plugin bitleri oluşturulur.
5.	Son olarak airsim’i kullanabilmek için bir Unreal Projesine ihtiyacımız vardır. Bunun için örnek olarak Airsim ile birlikte gelen “Blocks Environment” i kullanacağız.
Bu environment klasörü aşağıdaki dosya yolunda olabilir:
C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\AirSim\Unreal\Environments\Blocks

```
$ cd \Unreal\Environments\Blocks
$ update_from_git.bat
```
Bu komutlardan sonra klasrün içinde bir Blocks.sln solution dosyası oluşması gerekir.
Eğer aşağıdaki gibi bir Key hatası alındıysa muhtemelen Unreal Engine build’i ile ilgili bir sorun vardır.
```
Error: Cannot find path 'HKEY_CLASSES_ROOT\Unreal.ProjectFile\shell\rungenproj' because it does not exist
```

## How to Use It

### Documentation

View our [detailed documentation](https://microsoft.github.io/AirSim/) on all aspects of AirSim.

### Manual drive

If you have remote control (RC) as shown below, you can manually control the drone in the simulator. For cars, you can use arrow keys to drive manually.

[More details](https://microsoft.github.io/AirSim/remote_control/)

![record screenshot](docs/images/AirSimDroneManual.gif)

![record screenshot](docs/images/AirSimCarManual.gif)


### Programmatic control

AirSim exposes APIs so you can interact with the vehicle in the simulation programmatically. You can use these APIs to retrieve images, get state, control the vehicle and so on. The APIs are exposed through the RPC, and are accessible via a variety of languages, including C++, Python, C# and Java.

These APIs are also available as part of a separate, independent cross-platform library, so you can deploy them on a companion computer on your vehicle. This way you can write and test your code in the simulator, and later execute it on the real vehicles. Transfer learning and related research is one of our focus areas.

Note that you can use [SimMode setting](https://microsoft.github.io/AirSim/settings#simmode) to specify the default vehicle or the new [ComputerVision mode](https://microsoft.github.io/AirSim/image_apis#computer-vision-mode-1) so you don't get prompted each time you start AirSim.

[More details](https://microsoft.github.io/AirSim/apis/)

### Gathering training data

There are two ways you can generate training data from AirSim for deep learning. The easiest way is to simply press the record button in the lower right corner. This will start writing pose and images for each frame. The data logging code is pretty simple and you can modify it to your heart's content.

![record screenshot](docs/images/record_data.png)


### Paper

More technical details are available in [AirSim paper (FSR 2017 Conference)](https://arxiv.org/abs/1705.05065). Please cite this as:


