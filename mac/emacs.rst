emacs 问题
==============================

alt 按键问题
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: lisp

    (when (eq system-type 'darwin)
      ;; option 与 command 互换
      (setq mac-option-modifier 'super)
      (setq mac-command-modifier 'meta))
