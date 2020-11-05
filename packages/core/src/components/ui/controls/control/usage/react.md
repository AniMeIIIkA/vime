```tsx {3,24-33}
import React, { useMemo, useRef } from 'react';
import {
  VimeControl,
  VimeIcon,
  VimeTooltip,
  usePlayerContext,
} from '@vime/react';

function PlaybackControl() {
  const ref = useRef(null);
  const [paused, setPaused] = usePlayerContext(ref, 'paused', true);
  const [i18n] = usePlayerContext(ref, 'i18n', {});
  const icon = useMemo(() => (paused ? '#vime-play' : '#vime-pause'), [paused]);
  const tooltip = useMemo(() => (paused ? i18n.play : i18n.pause), [
    paused, 
    i18n,
  ]);
  
  const onClick = () => { 
    setPaused(false); 
  };

  return (
    <VimeControl
      keys="k"
      ref={ref}
      label={i18n.playback}
      pressed={paused}
      onClick={onClick}
    >
      <VimeIcon href={icon} />
      <VimeTooltip>{tooltip} (k)</VimeTooltip>
    </VimeControl>
  );
}
```
