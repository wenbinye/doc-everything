
使用 ::

    git clone https://github.com/gcuisinier/jenv.git ~/.jenv
    echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.bash_profile
    echo 'eval "$(jenv init -)"' >> ~/.bash_profile
    jenv add /System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home
    jenv add /Library/Java/JavaVirtualMachines/jdk17011.jdk/Contents/Home
    jenv versions
    jenv global oracle64-1.6.0.39
    jenv local oracle64-1.6.0.39
