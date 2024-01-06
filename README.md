## clone from https://github.com/OpenTalker/SadTalker  

### For MacOS M1

This method has been tested on a M1 MacbookPro (OS Sonoma 14.2, 32G Memery, 10CPU, 8GPU)

```bash
git clone https://github.com/jelly-liu/SadTalker4M1.git
cd SadTalker 
conda create -n sadtalker python=3.8
conda activate sadtalker
# install pytorch 2.0
pip install torch torchvision torchaudio
conda install ffmpeg
conda install numba
pip install -r requirements.txt
pip install dlib # macOS needs to install the original dlib.
```

### belows is some errors when install and running, for reference:
1. brew always download json file ... formula.jws.json, and very slow  
	try1 ok: ```bash export HOMEBREW_API_DOMAIN="https://mirrors.ustc.edu.cn/homebrew-bottles/api  ```  
	try2 ok: ```bash export HOMEBREW_NO_INSTALL_FROM_API=1```  
  recommand try1  
3. ImportError: Numba could not be imported  
	try ok: ```bash conda install numba ```  
4. when execute web-ui.sh, AttributeError: 'Row' object has no attribute 'style' #693  
	try no: ```bash pip uninstall gradio & pip install gradio==3.41.2```  
	try ok: use new app_sadtalker.zip.
here is the file: [app_sadtalker.zip](https://objects.githubusercontent.com/github-production-repository-file-5c1aeb/569518584/13259997?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20240106%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240106T032211Z&X-Amz-Expires=300&X-Amz-Signature=4c1ce64790a12447c9741c81aaaf1b877f91e367118eebeec50b60f9b885a49e&X-Amz-SignedHeaders=host&actor_id=15152867&key_id=0&repo_id=569518584&response-content-disposition=attachment%3Bfilename%3Dapp_sadtalker.zip&response-content-type=application%2Fx-zip-compressed)
5. Cannot load audio from file: `ffprobe` not found  
	try no: ```bash use admin to run web-ui.sh ```  
	try ok: ```bash conda install ffmpeg ```  
6. pip install TTS, error about sklearn:  
   because python3.8 conflict with scikit-learn, scikit-learn official site recommand python3.9.  
   under python 3.9, pip install TTS did success!!, but SadTalker need python3.8.  
   so, i commented the pip intall TTS in source code, you can use other AI-Voice to generate TTS voice.
   ```python
   launcher.py, line 191 and 192:
    # if sys.platform != 'win32' and not is_installed('tts'):
    #   run_pip(f"install TTS", "install TTS individually in SadTalker, which might not work on windows.")
   ```
8. ffmpeg error: Invalid argument, file in same place:
   Output results/8141d6d3-a2fa-4da5-9cfd-4f74b1eb6648/cute_little_girl##hello_full.mp4 same as Input #0 - exiting  
	 FFmpeg cannot edit existing files in-place.  
	 Error opening output file results/8141d6d3-a2fa-4da5-9cfd-4f74b1eb6648/cute_little_girl##hello_full.mp4.  
	 Error opening output files: Invalid argument  
	 Reason: It seems they're same, but ffmpeg can't overwrite (edit in-place) a file used as input.  
   So: do not care it, video already generated.
99. Finally, Enjoy!!

## here my test resault:
My Env: Macbook Pro M1, Sonoma 14.2.1, 32G memery, 10CPU(8+2), 8GPU.  
input 4 seconds voice.m4a, out 256*256 size video.  
it takes 30 minutes, very slow.  
CPU average usage 30%.  
GPU average usage 10%, it seems not use GPU.  
Memery average usage 20G.  
Very Very Very Slow.  
   
