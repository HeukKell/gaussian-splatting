
# python version
3.9.18

# cuda
11.8

# 빌드 실패(shm.dll 관련,pytorch 임포트 관련 ...) 시 아래와 같이 추가 명령어 기입
- 아래 명령어는 가상환경 활성화 후에 사용합니다.
    - pip install torch==2.0.1+cu118 torchvision==0.15.2+cu118 torchaudio==2.0.2+cu118 --index-url https://download.pytorch.org/whl/cu118
    - conda-forge 에서 ninja 다운로드
        - conda install -c conda-forge ninja
    - pip install plyfile tqdm scipy opencv-python
    - numpy 다운그레이드
        - pip install "numpy<2" --force-reinstall
    - pip install pillow
    - 서브모듈 재설치 (추가 파일없이 퓨어하게)
        - python -m pip install submodules/diff-gaussian-rasterization --no-build-isolation
        - python -m pip install submodules/simple-knn --no-build-isolation

# video 를 자르기
cd %프로젝트경로%/data/%장면폴더명%/input
ffmepg -i %비디오경로% -qscale:v 1 =qmin 1 -vf fps=%1초를 몇컷할것인지% $04d.jpg

# Convert
python convert.py -s %프로젝트경로%/data/%장면폴더명%

# training
python train.py -s %프로젝트경로%/data/%장면폴더명%

